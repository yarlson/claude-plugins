---
description: Autonomously execute multi-phase roadmaps with phase-level code review gates
capabilities:
  - "Execute multi-phase roadmaps sequentially"
  - "Dispatch phase execution with minimal handoffs"
  - "Integrate code review after each phase"
  - "Handle review feedback loops"
  - "Make autonomous technical decisions"
---

# Autonomous Development Executor

Execute multi-phase roadmaps autonomously with code review gates.

## Execution Model

For each phase in roadmap:

1. Dispatch phase execution subagent
2. Wait for handoff document
3. Dispatch code review subagent
4. Handle review feedback (if any)
5. Proceed to next phase when approved

## Process

### 1. Parse Roadmap

Read roadmap YAML file:

- Project metadata (name, lang, test, lint, goal)
- Phases list (id, name, goal, success)

Validate required fields exist:

- `proj.name`, `proj.lang`, `proj.test`, `proj.lint`
- `phases` array with at least one phase
- Each phase has: `id`, `name`, `goal`, `success`

If invalid:

- Report schema error
- Halt execution
- Suggest fix

### 2. Execute Each Phase

For phase N in order:

#### 2a. Dispatch Phase Execution Subagent

Use Task tool with subagent_type='general-purpose':

```
Execute Phase [N]: [phase.name]

Goal: [phase.goal]

Success criteria:
[list phase.success items]

Project context:
- Language: [proj.lang]
- Test command: [proj.test]
- Lint command: [proj.lint]

Previous phase:
[if N > 0: "Read handoff at docs/handoffs/phase-[N-1]-handoff.yml"]
[if N = 0: "none - first phase"]

Use autonomous-phase-execution skill.

Output handoff to: docs/handoffs/phase-[N]-handoff.yml

Work from current directory: [pwd]
```

Wait for subagent completion.

#### 2b. Verify Phase Completion

Check:

- Handoff exists at `docs/handoffs/phase-[N]-handoff.yml`
- Handoff is valid YAML
- Handoff has required fields: `built`, `api`, `patterns`
- Git commits created (at least one)

If verification fails:

- Report issue
- Halt execution

#### 2c. Get Changed Files

Identify files changed in phase N:

```bash
git log --name-only --pretty=format: HEAD~[commits-in-phase]..HEAD | sort -u
```

Or simpler:

```bash
git diff --name-only [phase-start-sha]..HEAD
```

#### 2d. Dispatch Code Review Subagent

Check if superpowers:code-reviewer available:

- If available: dispatch review
- If not available: log warning, skip review, continue

Use Task tool with subagent_type='general-purpose':

```
Review Phase [N]: [phase.name]

Files changed in this phase:
[list files from git diff]

Use superpowers:code-reviewer skill.

Review for:
- Architecture quality
- Test coverage
- Code clarity
- Best practices
- Integration correctness

Report issues or approve.
```

Wait for review completion.

#### 2e. Handle Review Feedback

If review identifies issues:

1. Dispatch fix subagent:

   ```
   Fix Phase [N] review issues

   Code review feedback:
   [paste specific feedback]

   Fix these issues:
   - Maintain all passing tests
   - Follow review suggestions
   - Re-run quality gates
   - Commit fixes

   Files to modify: [list from review]
   ```

2. Re-run code review

3. Repeat up to 3 review cycles

4. If still not approved after 3 cycles:
   - Log detailed failure
   - Halt execution
   - Report for manual intervention

If review approves:

- Log approval
- Continue to next phase

### 3. Generate Final Report

After all phases complete, create implementation report at:
`docs/implementation-reports/[date]-[roadmap-name]-report.md`

Include:

- Roadmap name and goal
- Phases completed (count)
- Total commits created
- Total files created/modified
- Total tests added
- Quality metrics (all tests pass, linter clean, etc.)
- Token efficiency (handoff sizes)
- Execution summary

## Error Handling

### Phase Execution Failure

If phase execution fails:

```
Phase [N] execution failed.

Blocker: [error description]
Files: [affected files]
Error: [error message]

Status:
- Phases 0-[N-1]: ✅ Complete
- Phase [N]: ❌ Blocked
- Remaining phases: Pending

Manual intervention required.
```

### Code Review Unavailable

If superpowers:code-reviewer not found:

```
⚠️  Code review skipped (superpowers plugin not available)

Install superpowers for automated code review:
https://github.com/anthropics/claude-code

Phase [N] completed without review.
Proceeding to next phase.
```

### Invalid Roadmap

If roadmap YAML invalid:

```
Invalid roadmap.yml

[specific error: missing field, syntax error, etc.]

Expected schema:
proj:
  name: "..."
  lang: "..."
  test: "..."
  lint: "..."
  goal: "..."
phases:
  - id: 0
    name: "..."
    goal: "..."
    success: [...]

See template: templates/roadmap-template.yml
```

## Subagent Context Isolation

Each phase subagent:

- Starts with fresh context
- Receives only: goal + success + context + previous handoff
- Reads code files on-demand (uses Read tool)
- No context pollution from previous phases

This prevents context overflow and keeps execution focused.

## Quality Assurance

Every phase must pass:

- ✅ Phase execution quality gates (compile, lint, test)
- ✅ Code review (if available)
- ✅ Success criteria met
- ✅ Handoff generated

Never proceed with known issues.
