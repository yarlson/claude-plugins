---
name: Interactive Roadmap Builder
description: Interactive roadmap creation through structured questioning, producing roadmaps optimized for autonomous development execution
when_to_use: when you need to create a multi-phase development roadmap from a rough idea or requirements
version: 1.0.0
---

# Interactive Roadmap Builder

## Overview

Transform rough project ideas into comprehensive, execution-ready roadmaps through structured questioning and incremental validation. Produces roadmaps optimized for the Autonomous Development Flow plugin.

**Core principle:** Ask questions to understand, break into phases, validate incrementally, produce actionable roadmap.

**Output:** A roadmap document saved to `docs/roadmaps/YYYY-MM-DD-<project-name>-roadmap.md`

## The Process

### Phase 1: Understanding the Project

Ask questions ONE at a time to gather:

**Project basics:**

- What problem are you solving?
- Who is the target user/audience?
- What's the core value proposition?

**Scope and constraints:**

- What are the must-have features?
- What's out of scope (nice-to-have but not now)?
- Any technical constraints? (language, framework, performance, etc.)
- Any time constraints?

**Success criteria:**

- How will you know the project is successful?
- What metrics matter?
- What quality standards must be met?

**Context:**

- Existing codebase or greenfield?
- Team size and skills?
- Dependencies on other systems?

**Prefer multiple choice when possible:**

```
What type of project is this?
A) New library/package
B) Web service/API
C) CLI tool
D) Desktop application
E) Other (please specify)
```

**Ask follow-up questions based on answers.**

### Phase 2: Phase Identification

Based on understanding, propose phase breakdown:

**Present 2-3 phase structure options:**

**Option A: Minimal phases (faster, riskier)**

```
Phase 0: Core functionality
Phase 1: Essential features
Phase 2: Polish and docs
```

**Option B: Balanced phases (recommended)**

```
Phase 0: Foundation and setup
Phase 1: Core feature A
Phase 2: Core feature B
Phase 3: Integration
Phase 4: Advanced features
Phase 5: Polish and documentation
```

**Option C: Granular phases (slower, safer)**

```
Phase 0: Project structure
Phase 1: Basic utilities
Phase 2: Core component A
Phase 3: Core component B
Phase 4: Component integration
Phase 5: Advanced feature A
Phase 6: Advanced feature B
Phase 7: Error handling
Phase 8: Documentation
Phase 9: Examples and guides
```

**Ask:** "Which phase structure feels right? Or would you like a different breakdown?"

**Based on choice, refine phases with user.**

### Phase 3: Phase Details Collection

For each phase identified, ask:

**Phase N: [Name]**

**Questions:**

1. "What's the main problem this phase solves?"
2. "What's the solution approach?"
3. "What are the success criteria? (How do we know it's done?)"
4. "Any specific implementation details or constraints?"
5. "Does this phase depend on anything from previous phases?"

**Present each phase incrementally:**

```
Here's what I have for Phase 0 so far:

Phase 0: Foundation and Setup
- Problem: Need project structure and basic utilities
- Solution: Create directory structure, testing framework, string utilities
- Success Criteria:
  • Directory structure created
  • Tests can run
  • Basic utilities working

Does this look right? Any changes?
```

**After validation, move to next phase.**

### Phase 4: Validation and Refinement

Present complete roadmap outline:

```markdown
# [Project Name] Roadmap

Overview: [Brief description]

## Phase 0: [Name]

**Problem:** [What needs solving]
**Solution:** [Approach]
**Success Criteria:** [How we know it's done]

## Phase 1: [Name]

...

[All phases listed]
```

**Ask:**

- "Does the phase order make sense?"
- "Are phases appropriately scoped? (not too big, not too small)"
- "Anything missing or should be removed?"
- "Any phases that should be split or combined?"

**Iterate until user is satisfied.**

### Phase 5: Phase Detail Enrichment

For each phase, expand with more details:

**Ask for each phase:**

1. "What are the key components/files needed?"
2. "What edge cases should be handled?"
3. "Any performance or security considerations?"
4. "Integration points with other phases?"
5. "Testing strategy for this phase?"

**Present enriched phase:**

```markdown
## Phase 2: Core Feature Implementation

**Problem Statement:**
Users need to [specific need]. Current approach [current limitation].

**Solution Overview:**
Implement [component] that provides [capability]. Use [approach/pattern]
to ensure [quality attribute].

**Success Criteria:**

- ✅ [Specific deliverable 1]
- ✅ [Specific deliverable 2]
- ✅ [Specific deliverable 3]
- ✅ All tests passing
- ✅ Documentation updated

**Implementation Details:**

- Component A: [description]
- Component B: [description]
- Use [library/pattern] for [reason]
- Handle [edge case] by [approach]

**Dependencies:**

- Requires Phase 0 (project setup) complete
- Requires Phase 1 (utilities) complete

**Testing Strategy:**

- Unit tests for [components]
- Integration tests for [interactions]
- Edge cases: [list]
```

**Validate:** "Does this phase description have enough detail for implementation?"

**Iterate through all phases.**

### Phase 6: Roadmap Metadata

Collect final metadata:

**Ask:**

1. "What's your target programming language?"
2. "Any specific testing framework preference?"
3. "Any linting/code quality tools to use?"
4. "Estimated time per phase? (optional)"
5. "Priority level for this project?"

**Add to roadmap header:**

```markdown
# [Project Name] Roadmap

**Status:** Ready for Execution
**Priority:** HIGH/MEDIUM/LOW
**Language:** [Language]
**Testing:** [Framework]
**Linting:** [Tool]
**Created:** YYYY-MM-DD

**Estimated Timeline:**

- Phase 0: [X hours]
- Phase 1: [Y hours]
  ...

**Total Estimated Time:** [Z hours]
```

### Phase 7: Final Review and Save

Present complete roadmap:

```markdown
[Full roadmap with all sections]
```

**Ask:** "This roadmap is ready. Should I save it?"

**If yes:**

- Save to `docs/roadmaps/YYYY-MM-DD-<project-name>-roadmap.md`
- Generate filename from project name (lowercase, hyphen-separated)
- Output summary:

  ```
  ✅ Roadmap saved!

  Location: docs/roadmaps/YYYY-MM-DD-project-name-roadmap.md
  Phases: X phases
  Total estimated time: Y hours

  Ready to execute with:
  /autonomous-dev docs/roadmaps/YYYY-MM-DD-project-name-roadmap.md

  Or review/edit the roadmap first and then execute.
  ```

## Roadmap Template Structure

### Complete Roadmap Format

````markdown
# [Project Name] Roadmap

**Status:** Ready for Execution
**Priority:** [HIGH/MEDIUM/LOW]
**Created:** YYYY-MM-DD
**Language:** [Programming Language]
**Testing Framework:** [e.g., pytest, jest, go test]
**Linting:** [e.g., ruff, eslint, golangci-lint]

**Project Goal:** [One sentence describing the ultimate objective]

**Target Audience:** [Who will use this]

**Success Metrics:**

- [Metric 1]
- [Metric 2]
- [Metric 3]

**Estimated Timeline:**

- Phase 0: [X hours]
- Phase 1: [Y hours]
- ...
- **Total:** [Z hours]

---

## Phase 0: [Phase Name]

**Problem Statement:**
[Detailed description of what problem this phase solves]

**Solution Overview:**
[High-level approach to solving the problem]

**Success Criteria:**

- ✅ [Specific, measurable outcome 1]
- ✅ [Specific, measurable outcome 2]
- ✅ [Specific, measurable outcome 3]
- ✅ All tests passing
- ✅ Documentation updated

**Implementation Details:**

- [Detail 1: what needs to be built]
- [Detail 2: key components]
- [Detail 3: technologies/patterns to use]
- [Detail 4: edge cases to handle]

**Dependencies:**

- [None for Phase 0, or list prerequisites]

**Testing Strategy:**

- Unit tests: [what to test]
- Integration tests: [what to test]
- Edge cases: [list specific scenarios]

**Estimated Effort:** [X hours]

---

## Phase 1: [Phase Name]

[Same structure as Phase 0]

---

[Continue for all phases]

---

## Testing Strategy (Overall)

**Unit Tests:**

- [Approach to unit testing across project]
- Coverage goal: [X%]

**Integration Tests:**

- [Approach to integration testing]
- Key scenarios: [list]

**End-to-End Tests:**

- [If applicable]

**Performance Tests:**

- [If applicable]

---

## Quality Standards

**Code Quality:**

- Follow [style guide]
- Use [type system/annotations]
- Maximum function complexity: [metric]
- Documentation: [requirements]

**Testing:**

- TDD approach (test first)
- Minimum coverage: [X%]
- All edge cases covered
- No flaky tests

**Documentation:**

- API documentation for all public interfaces
- Usage examples
- Architecture overview
- Contributing guide (if open source)

---

## Deliverables

After completing all phases:

**Source Code:**

- [Component 1]: [location]
- [Component 2]: [location]
- [Component 3]: [location]

**Tests:**

- [Test suite 1]: [location]
- [Test suite 2]: [location]

**Documentation:**

- README.md
- API documentation
- Examples
- Architecture docs

**Artifacts:**

- Package/build configuration
- CI/CD configuration (if applicable)
- Deployment guides (if applicable)

---

## Risk Analysis

**High Risks:**

- [Risk 1]: [Mitigation strategy]
- [Risk 2]: [Mitigation strategy]

**Medium Risks:**

- [Risk 3]: [Mitigation strategy]

**Low Risks:**

- [Risk 4]: [Mitigation strategy]

---

## Future Enhancements (Post-MVP)

Features intentionally deferred:

- [Feature 1]: [Reason for deferral]
- [Feature 2]: [Reason for deferral]
- [Feature 3]: [Reason for deferral]

---

**Ready for autonomous execution with:**

```bash
/autonomous-dev docs/roadmaps/YYYY-MM-DD-<project-name>-roadmap.md
```
````

```

## Question Techniques

### Opening Questions (Broad)

```

"Tell me about the project you want to build."

"What problem are you trying to solve?"

"Who will use this, and what will they achieve with it?"

```

### Narrowing Questions (Specific)

```

"For the data storage, would you prefer:
A) In-memory (fast, volatile)
B) File-based (persistent, simple)
C) Database (robust, scalable)
D) Let the implementation decide based on requirements"

"What's more important for this phase:
A) Speed of implementation
B) Robustness and error handling
C) Performance optimization
D) All equally important"

```

### Validation Questions

```

"I'm proposing these 5 phases. Does this breakdown make sense?"

"Phase 2 focuses on [X]. Is that the right scope, or should it include [Y]?"

"You mentioned [constraint]. How strict is this? Can we work around it if needed?"

```

### Clarification Questions

```

"When you say 'handle errors well', do you mean:
A) Graceful degradation
B) Detailed error messages for debugging
C) Retry logic
D) All of the above"

"For testing, should we:
A) Test everything extensively (slower, safer)
B) Focus on critical paths (balanced)
C) Minimal tests to validate (faster, riskier)"

```

## Phase Scoping Guidelines

### Good Phase Scope

**Characteristics:**
- Solves 1-3 related problems
- Can be completed in 2-8 hours
- Has clear success criteria
- Builds on previous phases
- Delivers working functionality

**Example:**
```

Phase 1: User Authentication

- Problem: Need secure user login
- Solution: JWT-based auth with password hashing
- Success: Users can register, login, logout with secure tokens
- Estimated: 4-6 hours

```

### Too Large (Split It)

**Signs:**
- Multiple unrelated features
- Takes more than 10 hours
- Success criteria list is too long
- Mixes foundation with features

**Example (Bad):**
```

Phase 1: Build Everything

- Authentication, API, database, frontend, deployment
- Success: Everything works
- Estimated: 40 hours

```

**Better (Split):**
```

Phase 0: Foundation (auth, database)
Phase 1: Core API
Phase 2: Frontend
Phase 3: Deployment

```

### Too Small (Combine It)

**Signs:**
- Takes less than 1 hour
- Trivial change
- Not a logical unit
- Creates unnecessary handoffs

**Example (Bad):**
```

Phase 1: Create user.py file
Phase 2: Add User class to user.py
Phase 3: Add login method to User class

```

**Better (Combined):**
```

Phase 1: User Authentication Model

- Create User class with authentication methods
- Success: User registration and login work

```

## Iterative Refinement

### Initial Pass

Get basic structure:
- Number of phases
- Phase names
- One-sentence descriptions

### Second Pass

Add detail:
- Problem statements
- Solution approaches
- Success criteria

### Third Pass

Enrich:
- Implementation details
- Dependencies
- Testing strategy

### Final Pass

Polish:
- Validate phase order
- Check phase scope
- Ensure clarity
- Add metadata

## Common Project Types

### Library/Package

**Typical phases:**
1. Core data structures/interfaces
2. Main functionality
3. Advanced features
4. Documentation and examples
5. Packaging and distribution

### Web Service/API

**Typical phases:**
1. Project setup and database
2. Authentication
3. Core endpoints
4. Business logic
5. Error handling and validation
6. Documentation (API docs)
7. Deployment configuration

### CLI Tool

**Typical phases:**
1. Argument parsing and configuration
2. Core functionality
3. Command implementations
4. Error handling and help text
5. Output formatting
6. Package and distribution

### Desktop Application

**Typical phases:**
1. UI framework setup
2. Main window and layout
3. Core features
4. Data persistence
5. Advanced features
6. Packaging and distribution

## Tips for Good Roadmaps

### ✅ Do

- **Be specific** in problem statements
- **Include measurable** success criteria
- **Order logically** (foundation → features → polish)
- **Keep phases focused** (1-3 main objectives)
- **Mention constraints** early (performance, security, etc.)
- **Plan for testing** in each phase
- **Document assumptions**
- **Consider edge cases**

### ❌ Don't

- Be vague ("make it better")
- Mix unrelated features in one phase
- Skip success criteria
- Ignore dependencies between phases
- Forget about testing
- Assume implementation details
- Create phases that are too large or too small
- Omit important constraints

## Example Dialogues

### Example 1: New Library

```

You: I want to build a JSON parsing library

Claude: Great! Let me understand the requirements. What problem does this solve that existing JSON libraries don't?

User: I need a fast, zero-allocation JSON parser for embedded systems

Claude: Interesting! What language?
A) C
B) Rust
C) Go
D) Other

User: C

Claude: For embedded systems, are there memory constraints I should know about?

User: Yes, maximum 64KB heap

Claude: Got it. What's the minimum feature set needed?
A) Parse only (read JSON)
B) Parse and serialize (read/write JSON)
C) Parse, serialize, and query (JSONPath-like)

User: Parse only for MVP

Claude: Perfect. Should it handle all JSON types or a subset?

[... continues with more questions ...]

Claude: Based on our discussion, I'm proposing this roadmap:

Phase 0: Core data structures (JSON node types, memory pools)
Phase 1: Tokenizer (lexical analysis)
Phase 2: Parser (syntax analysis)
Phase 3: API and error handling
Phase 4: Optimization (zero-allocation)
Phase 5: Testing and docs

Does this structure make sense?

```

### Example 2: Web Service

```

You: Need to build a task management API

Claude: What's the core functionality?
A) Basic CRUD for tasks
B) Task assignments and collaboration
C) Task scheduling and reminders
D) All of the above

User: Start with A, plan for B later

Claude: What about authentication?
A) No auth (open API)
B) API keys
C) JWT tokens with user accounts
D) OAuth

User: C

Claude: Database preference?
A) PostgreSQL
B) MySQL
C) MongoDB
D) SQLite (simpler)

User: PostgreSQL

[... more questions ...]

Claude: Here's the proposed roadmap:

Phase 0: Project setup (FastAPI, PostgreSQL connection, migrations)
Phase 1: User authentication (JWT, password hashing)
Phase 2: Task CRUD endpoints
Phase 3: Task filtering and search
Phase 4: Error handling and validation
Phase 5: API documentation (OpenAPI)
Phase 6: Deployment configuration

Sound good?

````

## Integration with Autonomous Development Flow

**After roadmap is complete:**

The roadmap is optimized for autonomous execution:
- Each phase has clear problem/solution/success criteria
- Implementation details guide the brainstorming phase
- Success criteria become test requirements
- Dependencies ensure correct phase ordering
- Testing strategy informs implementation approach

**User can immediately execute:**
```bash
/autonomous-dev docs/roadmaps/YYYY-MM-DD-project-roadmap.md
````

**The autonomous flow will:**

1. Read Phase 0 requirements
2. Create design (brainstorming)
3. Create plan (planning)
4. Implement with quality gates
5. Move to Phase 1
6. Repeat until complete

## Output Location

**Save roadmap to:**

```
docs/roadmaps/YYYY-MM-DD-<project-name>-roadmap.md
```

**Filename format:**

- Date prefix: YYYY-MM-DD
- Project name: lowercase, hyphen-separated
- Extension: .md

**Examples:**

- `docs/roadmaps/2025-11-19-json-parser-roadmap.md`
- `docs/roadmaps/2025-11-19-task-api-roadmap.md`
- `docs/roadmaps/2025-11-19-cli-tool-roadmap.md`

## Remember

- **One question at a time** during understanding phase
- **Use multiple choice** when possible for clarity
- **Validate incrementally** - don't wait until the end
- **Be flexible** - adjust phases based on feedback
- **Keep phases focused** - 1-3 objectives per phase
- **Make it actionable** - enough detail for autonomous execution
- **Consider the developer** - assume zero codebase context
- **Think about testing** - every phase needs tests
- **Plan for docs** - documentation is a deliverable

The goal is to create a roadmap that the autonomous development flow can execute with confidence!
