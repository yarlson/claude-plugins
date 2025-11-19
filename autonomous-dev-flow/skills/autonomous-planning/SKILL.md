---
name: Autonomous Planning
description: Create detailed implementation plans with bite-sized tasks from design documents, assuming zero codebase context
when_to_use: when design is complete and you need to create an actionable implementation plan
version: 1.0.0
---

# Autonomous Planning

## Overview

Transform design documents into comprehensive implementation plans with bite-sized, actionable tasks. Assume the engineer has zero context for the codebase but is skilled in software development.

**Core principle:** Break down designs into small, verifiable steps with complete context for each.

**Input:** Design document from autonomous brainstorming phase
**Output:** Implementation plan saved to `docs/plans/YYYY-MM-DD-<feature-name>-plan.md`

## Bite-Sized Task Granularity

**Each step is one action (2-5 minutes):**

- "Write the failing test" - step
- "Run it to make sure it fails" - step
- "Implement the minimal code to make the test pass" - step
- "Run the tests and make sure they pass" - step
- "Commit" - step

**Never:**

- Combine multiple actions into one step
- Write vague instructions like "add validation"
- Skip test-first workflow
- Defer testing to end

## Plan Document Structure

````markdown
# [Feature Name] Implementation Plan

> **Status:** Ready for implementation
> **Design:** docs/designs/YYYY-MM-DD-<feature-name>-design.md

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach from design]

**Tech Stack:** [Key technologies/libraries]

**Prerequisites:**

- [Any required setup]
- [Dependencies to install]
- [Environment configuration]

---

## Task 1: [Component Name]

**Objective:** [What this task accomplishes]

**Files:**

- Create: `exact/path/to/file.ext`
- Modify: `exact/path/to/existing.ext:123-145`
- Test: `tests/exact/path/to/test.ext`

**Background:**
[Brief context about this component and why it's needed]

### Step 1: Write the failing test

**File:** `tests/exact/path/to/test.ext`

```language
// Complete test code here
def test_specific_behavior():
    # Given
    setup = create_test_setup()

    # When
    result = function(input)

    # Then
    assert result == expected
```
````

**Why this test:** [Explain what behavior we're verifying]

### Step 2: Run test to verify it fails

**Command:**

```bash
pytest tests/path/test.ext::test_name -v
```

**Expected output:**

```
FAILED - NameError: function 'function' is not defined
```

**Why verify failure:** Ensures test actually tests the behavior (not false positive)

### Step 3: Write minimal implementation

**File:** `exact/path/to/file.ext`

```language
// Complete implementation code here
def function(input):
    """
    Brief description of what this does.

    Args:
        input: Description

    Returns:
        Description
    """
    # Implementation
    return expected
```

**Implementation notes:**

- [Any important details]
- [Edge cases handled]
- [Design patterns used]

### Step 4: Run test to verify it passes

**Command:**

```bash
pytest tests/path/test.ext::test_name -v
```

**Expected output:**

```
PASSED
```

### Step 5: Run full test suite

**Command:**

```bash
pytest tests/ -v
# or npm test, cargo test, go test ./..., etc.
```

**Expected:** All tests pass, no regressions

### Step 6: Commit

**Command:**

```bash
git add tests/path/test.ext src/path/file.ext
git commit -m "feat: add [specific feature]

- Implements [capability]
- Tests cover [scenarios]

Refs: #issue-number (if applicable)"
```

---

## Task 2: [Next Component]

[Same structure as Task 1]

---

## Integration Testing

After all tasks complete:

### Test: End-to-end workflow

**Objective:** Verify all components work together

**Command:**

```bash
# Complete test command
```

**Expected behavior:**

- [Specific outcome 1]
- [Specific outcome 2]
- [Specific outcome 3]

### Test: Error scenarios

**Objective:** Verify error handling

**Scenarios:**

1. [Error scenario 1] → [Expected behavior]
2. [Error scenario 2] → [Expected behavior]

---

## Verification Checklist

Before considering implementation complete:

- [ ] All unit tests pass
- [ ] Integration tests pass
- [ ] Error handling tested
- [ ] Code linted (zero warnings)
- [ ] Documentation updated
- [ ] Examples work
- [ ] Performance acceptable (if applicable)
- [ ] No regressions in existing functionality

---

## Rollback Plan

If issues discovered after integration:

1. **Immediate:** Revert to commit [specify stable commit]
2. **Diagnosis:** [How to diagnose what went wrong]
3. **Fix:** [General approach to fixing]
4. **Verification:** [How to verify fix works]

---

## Notes for Implementation

**Common pitfalls:**

- [Pitfall 1 and how to avoid]
- [Pitfall 2 and how to avoid]

**Performance considerations:**

- [If applicable]

**Security considerations:**

- [If applicable]

**Dependencies:**

- [External dependencies]
- [Version constraints]

---

**Next Steps:** Begin implementation with Task 1

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

- [ ] Every task has objective and context
- [ ] Every file path is exact and absolute
- [ ] Every code block is complete and runnable
- [ ] Every test has expected output
- [ ] Every commit message is provided
- [ ] Tasks ordered by dependencies
- [ ] Integration testing included
- [ ] Verification checklist included
- [ ] Rollback plan included
- [ ] Common pitfalls documented

## Save Location

Save to: `docs/plans/YYYY-MM-DD-<feature-name>-plan.md`

Use same feature name as design document for traceability.

## Integration with Next Phase

After saving plan, output summary:
- Path to saved plan
- Number of tasks
- Estimated time (task count × 15 minutes)
- Ready for implementation phase

## Remember

- Assume zero codebase knowledge
- Provide complete code, not snippets
- Exact paths, exact commands
- TDD all the way
- Small steps, frequent commits
- Verify everything
- DRY, YAGNI, SOLID
```
