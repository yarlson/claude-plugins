---
name: Autonomous Planning
description: Create detailed implementation plans with bite-sized tasks from design documents, assuming zero codebase context
when_to_use: when design is complete and you need to create an actionable implementation plan
version: 2.0.0
---

# Autonomous Planning

## Overview

Transform design documents into comprehensive implementation plans with bite-sized, actionable tasks. Assume the engineer has zero context for the codebase but is skilled in software development.

**Core principle:** Break down designs into small, verifiable steps with complete context for each.

**Input:** Design YAML document from autonomous brainstorming phase
**Output:** Implementation plan in YAML format saved to `docs/plans/YYYY-MM-DD-<feature-name>-plan.yml`

## Task Granularity

**Each task follows TDD structure:**

- `test`: Write the test code and file path
- `impl`: Write the implementation code and file path
- `commit`: Commit message

**The implementation agent will:**

1. Write test file
2. Run test (verify it fails)
3. Write implementation
4. Run test (verify it passes)
5. Run full test suite (verify no regressions)
6. Commit with provided message

**Never:**

- Combine multiple features into one task
- Write vague test cases
- Skip test-first workflow
- Defer testing to end

## Plan Document Structure

Create implementation plan as YAML with the following structure:

```yaml
meta:
  phase: 0
  name: "Foundation"
  design: "docs/designs/YYYY-MM-DD-<feature-name>-design.yml"
  created: "2025-12-08"

goal: "One sentence describing what this plan implements"

tech_stack:
  - "Python 3.9+"
  - "pytest for testing"
  - "ruff for linting"

prerequisites:
  - "Python 3.9+ installed"
  - "Virtual environment activated"
  - "Dependencies installed"

tasks:
  - name: "Calculator addition method"
    objective: "Implement add(a, b) with TDD"
    test:
      file: "tests/test_calculator.py"
      code: |
        import pytest
        from calculator import Calculator

        def test_add_positive():
            calc = Calculator()
            assert calc.add(2, 3) == 5

        def test_add_negative():
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

      - Implements addition
      - Full test coverage

  - name: "Calculator subtraction method"
    objective: "Implement subtract(a, b) with TDD"
    test:
      file: "tests/test_calculator.py"
      code: |
        def test_subtract():
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
  - name: "Full test suite"
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

## Planning Principles

**Complete Context:**

- Every task has all information needed
- No assumptions about prior knowledge
- Exact file paths, never relative or vague
- Complete code examples, not snippets

**Test-Driven:**

- Every task follows RED-GREEN-REFACTOR
- Tests written before implementation
- Tests verify behavior, not implementation
- Edge cases explicitly tested

**Granular:**

- Tasks are 10-20 minutes max
- Steps are 2-5 minutes each
- Frequent commits (after each passing test)
- Clear verification at each step

**Verifiable:**

- Every step has expected output
- Clear pass/fail criteria
- Commands are copy-pasteable
- No ambiguity in success

## Task Ordering

**Dependencies first:**

- Utilities before features
- Data structures before algorithms
- Interfaces before implementations
- Core before extensions

**Risk management:**

- High-risk/unknown tasks early
- Integration points early
- Performance-critical paths early
- Easy wins sprinkled throughout (morale)

**Logical grouping:**

- Related functionality together
- Complete vertical slices
- Minimize context switching

## Code Examples in Plans

**Always include:**

- Complete, runnable code
- Imports/dependencies
- Type annotations (if language supports)
- Docstrings/comments
- Error handling

**Never include:**

- Pseudocode
- "TODO" markers
- "Add your code here" placeholders
- Incomplete functions

## Testing Strategy

**Unit tests:**

- Test one function/method
- Mock external dependencies
- Fast execution
- Clear failure messages

**Integration tests:**

- Test components working together
- Minimal mocking
- Real(istic) data
- Cover critical paths

**Edge cases:**

- Empty inputs
- Null/nil values
- Boundary conditions
- Error conditions

## Commit Message Format

```

<type>: <brief summary in imperative mood>

<detailed explanation of what changed and why>

- Bullet points for specific changes
- Reference to design decisions if applicable

Refs: #issue-number

```

**Types:** feat, fix, refactor, test, docs, chore

## Anti-Patterns to Avoid

**In planning:**

- ❌ "Implement the feature" (too vague)
- ❌ "Add tests" (tests are integrated in TDD)
- ❌ "Fix any bugs" (not a planned task)
- ❌ Steps without verification
- ❌ Code without tests
- ❌ Vague file paths

**In tasks:**

- ❌ Multiple concepts in one task
- ❌ Tasks depending on future tasks
- ❌ Mixing refactoring with features
- ❌ Tests without clear assertions
- ❌ Implementation before tests

## Output Checklist

Before saving plan:

- [ ] Valid YAML syntax (proper indentation, quotes, pipes for code blocks)
- [ ] Meta section complete (phase, name, design path, created date)
- [ ] Every task has name, objective, test, impl, and commit
- [ ] Every file path is exact and absolute
- [ ] Every code block is complete and runnable
- [ ] Tasks ordered by dependencies
- [ ] Integration tests included
- [ ] Verification list included
- [ ] Tech stack and prerequisites documented

## Save Location

Save to: `docs/plans/YYYY-MM-DD-<feature-name>-plan.yml`

Use same feature name as design document for traceability.

**IMPORTANT:** Output as valid YAML. Use pipe (`|`) for multi-line code blocks. Proper indentation (2 spaces).

## Integration with Next Phase

After saving plan, output summary:

- Path to saved plan
- Number of tasks
- Estimated time (task count × 15 minutes)
- Ready for implementation phase

## Remember

- Output valid YAML format
- Assume zero codebase knowledge
- Provide complete code, not snippets
- Exact paths for all files
- Test/impl pairs for TDD workflow
- Complete commit messages
- DRY, YAGNI, SOLID principles
