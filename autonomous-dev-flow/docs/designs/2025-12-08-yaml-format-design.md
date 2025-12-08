# YAML Format Conversion Design

**Status:** Ready for Implementation
**Created:** 2025-12-08
**Goal:** Convert autonomous-dev-flow from verbose human-readable markdown to compact machine-readable YAML to reduce token consumption by 60-70%

---

## Overview

### Problem Statement

The autonomous-dev-flow plugin currently generates three document types in verbose markdown format:

- Roadmaps (input documents)
- Design documents (brainstorming output)
- Implementation plans (planning output)

These documents contain extensive prose, repeated explanations, and verbose formatting optimized for human readability. Since AI agents are the primary consumers of these documents, this verbosity causes:

- High token consumption (40K-60K+ tokens per roadmap execution)
- Slower processing
- Higher API costs
- Unnecessary context overhead

### Solution Overview

Replace markdown format with structured YAML for all three document types. YAML provides:

- 60-70% token reduction through compact syntax
- Structured data that's easier for agents to parse
- Essential information only, no verbose prose
- Machine-optimized while still debuggable

### Success Criteria

- ✅ All document types use YAML format (.yml extension)
- ✅ Token consumption reduced by 60-70%
- ✅ All skills/agents updated to read/write YAML
- ✅ Templates and examples use new format
- ✅ Documentation updated with YAML schemas
- ✅ Existing functionality preserved (no behavior changes)

---

## Architecture

### High-Level Approach

**Hard cutover strategy:**

- Remove all markdown generation code
- Replace with YAML generation
- Update all document readers to parse YAML
- Provide YAML templates and schema documentation
- No backward compatibility with .md files
- No conversion tools (users create new roadmaps)

**Component changes:**

1. **Skills** - Update to output YAML instead of markdown
2. **Agents** - Update to parse YAML documents
3. **Templates** - Replace .md templates with .yml templates
4. **Examples** - Replace .md examples with .yml examples
5. **Documentation** - Update with YAML schemas

### Technology Choices

**YAML over JSON:**

- More compact (no brackets/quotes for simple values)
- Better multi-line string support (code blocks)
- Still structured and parsable
- Debuggable if inspection needed

**YAML over custom format:**

- Standard, well-known format
- Built-in parsing in most languages
- Readable enough for debugging
- No custom parser needed

---

## Design Decisions

### Decision 1: Format All Documents as YAML

**Chosen:** Convert roadmaps, designs, and plans to YAML

**Rationale:**

- Roadmaps are also consumed by agents (not just written by users)
- Maximum token savings across the board
- Consistent format throughout the system
- Users can hand-write YAML roadmaps (simpler than prose)

**Alternatives considered:**

- Keep roadmaps as markdown - Rejected: Still verbose, agents read them
- Use JSON - Rejected: More verbose than YAML for code blocks

### Decision 2: Moderate Minimalism (Essentials Only)

**Chosen:** Keep essential information, remove verbose explanations

**Rationale:**

- Architecture decisions need rationale for planning phase
- Tasks need enough context for implementation
- Test/implementation structure preserves TDD workflow
- Balances token savings with agent decision-making needs

**Alternatives considered:**

- Preserve all info - Rejected: Only 30-40% savings
- Extreme minimalism - Rejected: Loses context for good decisions

### Decision 3: Hard Cutover (No Backward Compatibility)

**Chosen:** YAML only, no .md support, no conversion tool

**Rationale:**

- Cleaner codebase (no dual-format handling)
- Forces adoption of efficient format
- Simpler implementation and maintenance
- Plugin is new enough that few users have extensive .md libraries

**Alternatives considered:**

- Support both formats - Rejected: Code complexity, maintenance burden
- Provide converter - Rejected: Extra implementation work, encourages old format

---

## YAML Schemas

### Roadmap Schema

```yaml
# roadmap.yml
project:
  name: "Project Name"
  language: "Python" # Go, Rust, TypeScript, etc.
  testing: "pytest" # go test, cargo test, jest, etc.
  linting: "ruff" # golangci-lint, clippy, eslint, etc.
  goal: "One sentence project objective"

phases:
  - id: 0
    name: "Foundation"
    goal: "Create utilities and structure"
    success:
      - "Directory structure created"
      - "String utilities working"
      - "Tests passing"

  - id: 1
    name: "Core Feature"
    goal: "Implement main feature logic"
    success:
      - "Tokenizer working"
      - "Parser generates AST"
      - "All tests passing"
```

**Key reductions:**

- No separate "Problem Statement" / "Solution Overview" prose (combined into "goal")
- No "Implementation Details" section (brainstorming phase figures this out)
- No "Testing Strategy" per phase (covered in success criteria)
- No estimated timeline (not needed for execution)

### Design Document Schema

```yaml
# design.yml
meta:
  phase: 0
  name: "Foundation"
  created: "2025-12-08"

goal: "One sentence: what this phase accomplishes"

architecture: |
  2-3 paragraphs describing high-level architecture.
  Component relationships, data flow, key patterns.

decisions:
  - choice: "Use SQLite"
    rationale: "Simple, embedded, sufficient for MVP"
    alternatives:
      - option: "PostgreSQL"
        rejected: "Overkill for MVP, deployment complexity"
      - option: "In-memory"
        rejected: "Data not persisted"

  - choice: "MVC pattern"
    rationale: "Separation of concerns, testability"
    alternatives:
      - option: "Monolithic"
        rejected: "Hard to test, poor separation"

components:
  - name: "Calculator"
    purpose: "Core arithmetic operations"
    interface:
      - "add(a, b) -> float"
      - "subtract(a, b) -> float"
    dependencies: []

  - name: "Parser"
    purpose: "Parse expression strings into operations"
    interface:
      - "parse(expr: str) -> AST"
    dependencies: ["Calculator"]

error_handling:
  - scenario: "Division by zero"
    strategy: "Raise ZeroDivisionError with clear message"
  - scenario: "Invalid expression"
    strategy: "Raise ValueError with parsing context"

testing:
  unit: "Test each component method in isolation with mocks"
  integration: "Test Calculator + Parser workflow end-to-end"
  edge_cases:
    - "Empty inputs"
    - "Null/None values"
    - "Boundary conditions (very large/small numbers)"
```

**Key reductions:**

- No verbose "Overview" section (goal is concise)
- No "Design Decisions" prose (structured choice/rationale/alternatives)
- No "Component Details" prose (structured fields)
- No "Implementation Considerations" section (covered in components/error_handling)
- No "Future Enhancements" (not needed for implementation)

### Implementation Plan Schema

```yaml
# plan.yml
meta:
  phase: 0
  name: "Foundation"
  design: "docs/designs/2025-12-08-foundation-design.yml"
  created: "2025-12-08"

goal: "One sentence: what this plan implements"

tech_stack:
  - "Python 3.9+"
  - "pytest"
  - "ruff"

prerequisites:
  - "Python 3.9+ installed"
  - "Virtual environment activated"

tasks:
  - name: "Calculator addition method"
    objective: "Implement add(a, b) with TDD"
    test:
      file: "tests/test_calculator.py"
      code: |
        def test_add_positive_numbers():
            calc = Calculator()
            assert calc.add(2, 3) == 5

        def test_add_negative_numbers():
            calc = Calculator()
            assert calc.add(-2, -3) == -5

    impl:
      file: "src/calculator.py"
      code: |
        class Calculator:
            def add(self, a: float, b: float) -> float:
                """Add two numbers."""
                return a + b

    commit: |
      feat: add Calculator.add() method

      - Implements addition for positive and negative numbers
      - Full test coverage

  - name: "Calculator subtraction method"
    objective: "Implement subtract(a, b) with TDD"
    test:
      file: "tests/test_calculator.py"
      code: |
        def test_subtract_positive_numbers():
            calc = Calculator()
            assert calc.subtract(5, 3) == 2

    impl:
      file: "src/calculator.py"
      code: |
        def subtract(self, a: float, b: float) -> float:
            """Subtract b from a."""
            return a - b

    commit: |
      feat: add Calculator.subtract() method

      - Implements subtraction
      - Full test coverage

integration:
  - name: "Full calculator workflow"
    command: "pytest tests/ -v"
    expect: "All tests pass"

  - name: "Linting"
    command: "ruff check ."
    expect: "No issues"

verification:
  - "All unit tests pass"
  - "Integration tests pass"
  - "Code lints with zero warnings"
  - "No regressions"
```

**Key reductions:**

- No verbose "Background" section per task
- No step-by-step TDD breakdown (implementation agent knows TDD flow)
- No "Expected output" for each step (agent verifies pass/fail)
- No "Why this test" explanations
- No "Implementation notes" prose
- No "Verification Checklist" (covered in verification list)
- No "Rollback Plan" (standard git practices)
- No "Notes for Implementation" / "Common Pitfalls" (kept simple)

---

## Component Details

### Component 1: Autonomous Brainstorming Skill

**File:** `skills/autonomous-brainstorming/SKILL.md`

**Changes:**

- Replace markdown generation with YAML generation
- Output file extension: `.md` → `.yml`
- Use YAML schema defined above
- Remove verbose prose sections
- Structure decisions as choice/rationale/alternatives
- Keep architecture as multi-line string (needs prose)

**Interface:**

- Input: Phase requirements from roadmap YAML
- Output: Design YAML file at `docs/designs/YYYY-MM-DD-<name>-design.yml`

### Component 2: Autonomous Planning Skill

**File:** `skills/autonomous-planning/SKILL.md`

**Changes:**

- Replace markdown generation with YAML generation
- Output file extension: `.md` → `.yml`
- Use YAML schema defined above
- Structure tasks as test/impl pairs (no verbose steps)
- Remove "Background" and "Why" explanations
- Assume agent knows TDD flow (write test → verify fail → implement → verify pass → commit)

**Interface:**

- Input: Design YAML file
- Output: Plan YAML file at `docs/plans/YYYY-MM-DD-<name>-plan.yml`

### Component 3: Roadmap Builder Skill

**File:** `skills/roadmap-builder/SKILL.md`

**Changes:**

- Generate YAML roadmap instead of markdown
- Output file extension: `.md` → `.yml`
- Use YAML schema defined above
- Prompt for: project name, language, testing/linting tools, phases with goals and success criteria
- Remove verbose problem/solution prose
- Streamline to goal + success criteria per phase

**Interface:**

- Input: Interactive user questions
- Output: Roadmap YAML file at `docs/roadmaps/YYYY-MM-DD-<name>-roadmap.yml`

### Component 4: Autonomous Executor Agent

**File:** `agents/autonomous-executor.md`

**Changes:**

- Parse roadmap as YAML instead of markdown
- Read roadmap file with YAML parser
- Extract phases from `phases` list
- Pass phase `goal` and `success` to brainstorming
- Read design/plan YAML files (not markdown)

**Dependencies:**

- YAML parsing capability (standard library in most languages)

### Component 5: Autonomous Implementation Skill

**File:** `skills/autonomous-implementation/SKILL.md`

**Changes:**

- Parse plan as YAML instead of markdown
- Extract tasks from `tasks` list
- For each task:
  - Write test file (`task.test.file` with `task.test.code`)
  - Run test, verify failure
  - Write implementation (`task.impl.file` with `task.impl.code`)
  - Run test, verify pass
  - Commit with message (`task.commit`)
- Run integration tests from `integration` list
- Verify against `verification` checklist

**Dependencies:**

- YAML parsing capability

### Component 6: Templates and Examples

**Files:**

- `templates/roadmap-template.md` → `templates/roadmap-template.yml`
- `examples/simple-roadmap.md` → `examples/simple-roadmap.yml`

**Changes:**

- Convert to YAML format
- Follow schemas defined above
- Add inline comments explaining each section
- Provide complete, copy-pasteable examples

---

## Error Handling

### Invalid YAML Syntax

**Scenario:** Roadmap/design/plan file has syntax errors

**Strategy:**

- Agent catches YAML parse error
- Reports specific error message (line number, syntax issue)
- Halts execution with clear guidance

**User-facing message:**

```
Error: Invalid YAML syntax in roadmap file
  File: docs/roadmaps/2025-12-08-my-roadmap.yml
  Line: 15
  Issue: Incorrect indentation

Please fix YAML syntax and try again.
Validate at: https://www.yamllint.com/
```

### Missing Required Fields

**Scenario:** YAML file missing required fields (e.g., no `phases` in roadmap)

**Strategy:**

- Validate required fields after parsing
- Report missing fields with expected schema
- Halt execution

**User-facing message:**

```
Error: Invalid roadmap schema
  Missing required field: phases

Expected schema:
  project: {...}
  phases: [...]
```

### File Not Found

**Scenario:** Referenced design/plan file doesn't exist

**Strategy:**

- Check file existence before parsing
- Report missing file with expected path
- Halt execution

**User-facing message:**

```
Error: Design file not found
  Expected: docs/designs/2025-12-08-foundation-design.yml

Run brainstorming phase first to generate design.
```

---

## Testing Strategy

### Unit Testing

Not applicable - this is a documentation format change, not code logic

### Integration Testing

**Test 1: End-to-end roadmap execution**

- Create minimal YAML roadmap (1 phase, simple feature)
- Run `/autonomous-dev roadmap.yml`
- Verify:
  - Design YAML generated
  - Plan YAML generated
  - Implementation completes
  - All files are valid YAML

**Test 2: YAML parsing**

- Create test YAML files with all schema features
- Verify agents can parse correctly
- Extract expected fields

**Test 3: Error handling**

- Test invalid YAML syntax
- Test missing required fields
- Test file not found
- Verify clear error messages

### Manual Testing

- Convert simple-roadmap.md to YAML
- Run autonomous development
- Compare token usage before/after
- Verify generated YAML is valid
- Check that implementation works correctly

---

## Implementation Considerations

### Challenge 1: YAML Multi-line Strings

**Issue:** Code blocks need proper YAML formatting

**Solution:** Use pipe (`|`) for literal multi-line strings:

```yaml
code: |
  def test_add():
      assert calc.add(2, 3) == 5
```

### Challenge 2: Indentation Sensitivity

**Issue:** YAML is whitespace-sensitive, errors can be subtle

**Solution:**

- Use 2-space indentation consistently
- Add validation step in agents (parse, catch errors)
- Provide clear error messages with line numbers

### Challenge 3: Agent Prompt Changes

**Issue:** Skills reference markdown sections that no longer exist

**Solution:**

- Update skill prompts to reference YAML structure
- Change "Write to section X" → "Set field Y"
- Update examples in skills

### Challenge 4: Template Clarity

**Issue:** YAML templates need to be self-documenting

**Solution:**

- Add inline comments in templates
- Provide complete working examples
- Include schema documentation in README

---

## Migration Path

### For Users with Existing .md Files

**Option 1: Manual recreation**

- Create new YAML roadmap following template
- Copy over phase goals and success criteria
- Simplified structure makes this quick

**Option 2: Continue with old version**

- No conversion tool provided
- Hard cutover means old format won't work
- Users must migrate or stay on old version

### For Plugin Development

**Phase 1: Update schemas (Priority 1)**

1. Create YAML templates
2. Update README with schemas
3. Create example YAML files

**Phase 2: Update skills (Priority 2)** 4. Update autonomous-brainstorming → output YAML 5. Update autonomous-planning → output YAML 6. Update roadmap-builder → output YAML

**Phase 3: Update agents (Priority 3)** 7. Update autonomous-executor → parse YAML 8. Update autonomous-implementation → parse YAML

**Phase 4: Cleanup (Priority 4)** 9. Remove old .md templates 10. Update all documentation references 11. Test end-to-end

---

## Token Savings Estimate

### Current Markdown (Example)

**Roadmap:** ~3,000 tokens (6 phases with verbose descriptions)
**Design:** ~4,000 tokens (architecture prose, verbose decisions)
**Plan:** ~8,000 tokens (step-by-step TDD, explanations)
**Total per phase:** ~15,000 tokens

### Proposed YAML (Example)

**Roadmap:** ~800 tokens (structured fields, no prose)
**Design:** ~1,500 tokens (structured decisions, concise)
**Plan:** ~2,500 tokens (test/impl pairs, no verbose steps)
**Total per phase:** ~4,800 tokens

### Savings

**Per phase:** 68% reduction (15,000 → 4,800 tokens)
**6-phase roadmap:** ~60,000 → ~20,000 tokens (67% savings)

---

## Future Enhancements

Features intentionally deferred:

### 1. YAML Validation CLI

- Standalone command to validate YAML files against schema
- Useful for debugging and pre-flight checks
- Not critical for MVP (agents handle errors)

### 2. Markdown to YAML Converter

- Automated tool to convert legacy .md files
- Helpful if user adoption requires it
- Not building now (clean break strategy)

### 3. YAML Schema Files

- Formal JSON Schema or YAML Schema for validation
- Enables IDE autocomplete and validation
- Nice-to-have, not critical

---

## Success Metrics

**Primary:**

- Token consumption reduced by 60%+ (measured in test execution)

**Secondary:**

- All existing functionality works with YAML
- Documentation clear enough for users to create YAML roadmaps
- No increase in errors or failures

**Quality:**

- Valid YAML generated in all cases
- Error messages clear and actionable
- Templates and examples work as-is

---

**Next Steps:** Proceed to implementation planning phase
