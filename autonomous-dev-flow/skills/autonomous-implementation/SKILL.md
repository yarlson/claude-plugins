---
name: Autonomous Implementation
description: Execute implementation plans by dispatching subagents for each task with automatic verification and quality gates
when_to_use: when you have a complete implementation plan and need to execute it autonomously
version: 2.0.0
---

# Autonomous Implementation

## Overview

Execute YAML implementation plans by dispatching fresh subagents for each task, with automatic verification and quality gates. No user interaction required.

**Core principle:** Fresh subagent per task + automatic verification + quality gates = reliable autonomous execution

**Input:** YAML implementation plan from autonomous planning phase
**Output:** Fully implemented and tested feature, ready for review

## Quality Gates (ALL must pass)

Before any commit:

1. ✅ Code compiles without errors
2. ✅ Linter passes (0 issues)
3. ✅ All tests pass (0 failures)
4. ✅ No regressions in existing functionality

**If ANY quality gate fails:**

- DO NOT commit
- Fix the issue immediately
- Re-run quality gates
- NEVER rationalize broken builds

## The Process

### 1. Load and Parse YAML Plan

- Read YAML implementation plan file
- Parse YAML structure to extract:
  - Tech stack and prerequisites
  - Tasks list with test/impl pairs
  - Integration tests
  - Verification checklist
- Create internal task list from `tasks` array

### 2. For Each Task: Dispatch Implementation Subagent

**Extract task details from YAML:**

```yaml
# From tasks[N]:
name: "Task name"
objective: "What to accomplish"
test:
  file: "tests/path/to/test.py"
  code: |
    # Complete test code
impl:
  file: "src/path/to/impl.py"
  code: |
    # Complete implementation code
commit: |
  Commit message
```

**Subagent prompt:**

```
You are implementing: [task.name]
Objective: [task.objective]

Task details from YAML plan:

Test file: [task.test.file]
Test code:
[task.test.code]

Implementation file: [task.impl.file]
Implementation code:
[task.impl.code]

Commit message:
[task.commit]

Your job:

1. **Follow TDD strictly:**
   - Write test to [task.test.file]
   - Run test, verify it FAILS
   - Write implementation to [task.impl.file]
   - Run test, verify it PASSES
   - Run full test suite, verify NO REGRESSIONS

2. **Quality gates (ALL must pass before commit):**
   - ✅ Code compiles without errors
   - ✅ Linter passes (zero issues)
   - ✅ All tests pass (zero failures)
   - ✅ No regressions

3. **Verification commands:**
   - Compile: [language-specific build command]
   - Lint: [language-specific lint command]
   - Test: [language-specific test command]

4. **Commit only when ALL quality gates pass**
   - Use exact commit message from task
   - Include test and implementation files

5. **Report back:**
   - What you implemented
   - Compilation status (✅/❌)
   - Linter status (✅/❌)
   - Test results (X/Y passed)
   - Files changed
   - Commit SHA
   - Any issues encountered

**CRITICAL RULES:**
- NEVER commit code that doesn't compile
- NEVER commit code with linter errors
- NEVER commit code with failing tests
- NEVER skip quality gate verification
- If you cannot fix an issue, report it and STOP

Work from: [project-directory]
```

**Wait for subagent to complete and report.**

### 3. Verify Subagent's Work

Check subagent report for:

- ✅ All quality gates passed
- ✅ Commit created with correct message
- ✅ All files from plan were modified
- ✅ Tests added and passing

**If verification fails:**

- Dispatch fix subagent with specific instructions
- Re-verify after fix
- Repeat until quality gates pass

**If subagent cannot proceed:**

- Log blocker
- Attempt fix with focused subagent
- If still blocked, escalate (this should be rare)

### 4. Mark Task Complete

- Update internal task list
- Record commit SHA
- Move to next task

### 5. After All Tasks: Integration Verification

**Extract integration tests from YAML plan:**

```yaml
# From plan YAML:
integration:
  - name: "Full test suite"
    command: "pytest tests/ -v"
    expect: "All tests pass"
  - name: "Linting"
    command: "ruff check ."
    expect: "No issues"
```

**Dispatch integration verification subagent:**

```
All tasks from [plan-file-path] are complete.

Your job is to verify the integration using tests from YAML plan:

Integration tests to run:
[For each item in integration list]
- Name: [integration[N].name]
- Command: [integration[N].command]
- Expected: [integration[N].expect]

Verification checklist from plan:
[Each item from verification list]

Your steps:

1. **Run each integration test command**
   - Execute command
   - Compare output with expected result
   - Record pass/fail

2. **Verify checklist items**
   - All unit tests pass
   - Integration tests pass
   - Code lints with zero warnings
   - No regressions
   - [Additional items from plan]

3. **Report:**
   - Integration test results (pass/fail for each)
   - Checklist verification results
   - Any failures or issues
   - Performance observations
   - Recommendations

If ANY integration test fails:
- Identify root cause
- Propose fix
- DO NOT proceed until resolved
```

**Wait for integration verification report.**

### 6. Handle Integration Issues

**If integration verification fails:**

- Analyze failure cause
- Dispatch targeted fix subagent
- Re-run integration verification
- Repeat until all tests pass

**Common integration issues:**

- Interface mismatches between components
- Missing edge case handling
- Race conditions
- Resource leaks
- Performance bottlenecks

### 7. Final Quality Check

Run complete quality check:

```bash
# Compile
[language-specific build command]

# Lint entire codebase
[language-specific lint with --fix if available]

# Test everything
[language-specific test command with coverage]

# Check for common issues
- No TODOs in committed code
- No debug print statements
- No commented-out code
- No merge conflict markers
- All imports used
- No unused variables
```

**All checks must pass.**

### 8. Generate Summary Report

Create summary of implementation:

```markdown
# Implementation Complete: [Feature Name]

## Overview

- **Plan:** docs/plans/YYYY-MM-DD-feature-name-plan.md
- **Design:** docs/designs/YYYY-MM-DD-feature-name-design.md
- **Tasks completed:** X/X
- **Commits:** X commits
- **Tests added:** X tests, all passing
- **Files changed:** X files

## Commits

- [SHA] feat: [description]
- [SHA] feat: [description]
- [SHA] feat: [description]

## Test Coverage

- Unit tests: X tests, all passing
- Integration tests: X tests, all passing
- Edge cases covered: [list]

## Quality Gates

- ✅ Compilation: Clean
- ✅ Linter: Zero issues
- ✅ Tests: X/X passing
- ✅ No regressions

## Files Changed

- Created: [list]
- Modified: [list]
- Tests added: [list]

## Verification

- [✅] All planned functionality implemented
- [✅] All tests passing
- [✅] Error handling working
- [✅] Integration tests passing
- [✅] Performance acceptable
- [✅] Documentation updated

## Next Steps

Ready for review and merge to main branch.

## Notes

[Any important notes, caveats, or considerations]
```

Save summary to: `docs/implementation-reports/YYYY-MM-DD-feature-name-report.md`

### 9. Complete

Output summary and completion status.

## Language-Specific Commands

### Go

```bash
# Compile
go build ./...

# Lint
golangci-lint run --fix ./...

# Test
go test ./... -race -cover
```

### Python

```bash
# Lint
ruff check --fix .
mypy .

# Test
pytest tests/ -v --cov

# Type check
pyright
```

### Rust

```bash
# Compile
cargo build

# Lint
cargo clippy --all-targets --all-features -- -D warnings

# Test
cargo test

# Format
cargo fmt --check
```

### TypeScript/JavaScript

```bash
# Lint
eslint --fix .

# Type check (TS)
tsc --noEmit

# Test
npm test
# or
jest --coverage
```

### Java

```bash
# Compile
mvn compile

# Lint
mvn checkstyle:check

# Test
mvn test
```

## Error Handling

### Compilation Errors

**If subagent reports compilation error:**

1. Check if error is expected (e.g., test step 2)
2. If unexpected:
   - Read error message
   - Identify cause
   - Dispatch fix subagent with specific context
   - Re-verify compilation

### Test Failures

**If tests fail unexpectedly:**

1. Identify which tests failed
2. Read failure messages
3. Determine if:
   - Bug in implementation
   - Bug in test
   - Missing dependency
   - Environment issue
4. Dispatch focused fix subagent
5. Re-run tests

### Linter Errors

**If linter reports issues:**

1. Try auto-fix first: `[linter] --fix`
2. If auto-fix insufficient:
   - Read linter messages
   - Categorize (style, bug, complexity)
   - Fix manually or dispatch fix subagent
3. Re-run linter

### Integration Failures

**If integration tests fail:**

1. Identify which integration failed
2. Check component interfaces
3. Verify data flow
4. Check for:
   - Missing error handling
   - Race conditions
   - State management issues
   - Dependency issues
5. Dispatch debugging subagent
6. Apply fixes
7. Re-test integration

## Subagent Management

### Fresh Subagent Per Task

**Why:** Prevents context pollution, maintains focus, enables parallel-safe execution

**How:** Use Task tool with general-purpose subagent for each task

### Sequential Execution

**Why:** Ensures tasks build on completed work, prevents conflicts

**How:** Wait for task N to complete before starting task N+1

### Focused Fix Subagents

**When:** Quality gate fails or integration issues

**How:** Dispatch with specific problem and context

**Example:**

```
Fix the compilation error in [file.ext]:

Error message:
[exact error]

Context:
- We just implemented [feature]
- Expected behavior: [description]
- This error is blocking task N

Your job:
1. Read the file and understand the error
2. Fix the minimal issue causing the error
3. Verify compilation succeeds
4. Do NOT modify anything else
5. Commit the fix
6. Report back
```

## Decision Making

### When to Retry

**Retry if:**

- Transient error (network, file system)
- Clear fix available
- Retry count < 3

**Don't retry if:**

- Fundamental design issue
- Blocker in dependencies
- Ambiguous plan instructions

### When to Stop

**Stop and report if:**

- Cannot meet quality gates after 3 attempts
- Plan instructions ambiguous/incorrect
- Missing critical dependency
- Design flaw discovered
- External blocker

## Verification Principles

### Verify Everything

**Before committing:**

- Compilation ✅
- Linting ✅
- Unit tests ✅
- Integration tests ✅

**After each task:**

- Task objectives met ✅
- No regressions ✅
- Code quality maintained ✅

**After all tasks:**

- End-to-end scenarios ✅
- Error handling ✅
- Performance acceptable ✅
- Documentation current ✅

### Evidence Before Assertions

**Never assume:**

- "Tests probably pass"
- "Should compile fine"
- "Lint likely clean"

**Always verify:**

- Run the command
- Check the output
- Confirm success criteria

## Anti-Patterns to Avoid

**Never:**

- Skip quality gates
- Commit failing code
- Proceed with known issues
- Batch multiple tasks without verification
- Assume tests pass without running
- Skip integration testing
- Commit without linting
- Ignore warnings

**Always:**

- Verify every quality gate
- Fix issues before proceeding
- Run full test suite
- Check for regressions
- Lint before committing
- Test integration thoroughly
- Follow TDD strictly

## Success Criteria

Implementation is complete when:

- ✅ All planned tasks implemented
- ✅ All quality gates passed
- ✅ All tests passing (unit + integration)
- ✅ Zero linter issues
- ✅ Clean compilation
- ✅ No regressions
- ✅ Error scenarios tested
- ✅ Documentation updated
- ✅ Summary report generated
- ✅ Ready for review

## Output Format

After completion:

```
Implementation complete!

Summary report: docs/implementation-reports/YYYY-MM-DD-feature-name-report.md

Key metrics:
- Tasks: X/X completed
- Commits: X commits
- Tests: X new tests, all passing
- Files: X files changed
- Quality: ✅ All gates passed

Ready for phase transition to next phase of roadmap.
```

## Remember

- Fresh subagent per task (isolation)
- Quality gates are non-negotiable
- Verify everything, assume nothing
- Fix issues immediately, don't accumulate
- TDD all the way
- Small commits, frequent verification
- Integration testing is critical
- Document as you go
