---
name: Autonomous Brainstorming
description: Transform rough requirements into fully-formed designs autonomously, making informed decisions based on best practices and DX principles
when_to_use: when you need to refine requirements into a design document without user interaction
version: 2.0.0
---

# Autonomous Brainstorming

## Overview

Transform requirements into fully-formed designs through autonomous analysis and decision-making, optimizing for best current and future developer experience (DX).

**Core principle:** Analyze requirements, explore alternatives internally, select the best approach, document comprehensively.

**Output:** A design document in YAML format saved to `docs/designs/YYYY-MM-DD-<feature-name>-design.yml`

## The Process

### Phase 1: Understanding

- Read and analyze the requirements thoroughly
- Identify: Purpose, constraints, success criteria
- List assumptions and design constraints
- Check current project state and architecture

### Phase 2: Internal Exploration

Internally evaluate 2-3 different approaches:

For each approach, consider:

- Core architecture and components
- Trade-offs (complexity, maintainability, performance)
- Alignment with best practices
- Future extensibility
- Developer experience impact

**Selection criteria:**

- Simplicity and clarity (YAGNI, DRY)
- Maintainability
- Testability
- Performance where it matters
- Future flexibility
- Best practices alignment

### Phase 3: Design Document Creation

Create comprehensive YAML design document with the following structure:

**Meta Information:**

- `meta.phase`: Phase number
- `meta.name`: Phase name
- `meta.created`: Current date (YYYY-MM-DD)

**Goal:**

- One sentence describing what this phase accomplishes

**Architecture:**

- High-level architecture (2-3 paragraphs as multi-line string)
- Component relationships, data flow, key patterns

**Decisions:**

- List of architecture/technology decisions
- Each decision includes:
  - `choice`: What was chosen
  - `rationale`: Why this choice was made
  - `alternatives`: List of options considered and rejected
    - `option`: Alternative considered
    - `rejected`: Why it was rejected

**Components:**

- List of major components
- Each component includes:
  - `name`: Component name
  - `purpose`: What it does
  - `interface`: List of method signatures
  - `dependencies`: List of other components it depends on

**Error Handling:**

- List of error scenarios
- Each includes:
  - `scenario`: What error can occur
  - `strategy`: How to handle it

**Testing:**

- `unit`: Unit testing approach (string)
- `integration`: Integration testing approach (string)
- `edge_cases`: List of edge cases to cover

### Phase 4: Save Design Document

Save to: `docs/designs/YYYY-MM-DD-<feature-name>-design.yml`

Use clear, descriptive feature name (lowercase, hyphen-separated).

**IMPORTANT:** Output as valid YAML. Use pipe (`|`) for multi-line strings (architecture section). Proper indentation (2 spaces).

## Design Principles to Apply

**YAGNI (You Aren't Gonna Need It):**

- Build only what's needed now
- Avoid speculative features
- Prefer simple solutions

**DRY (Don't Repeat Yourself):**

- Identify and eliminate duplication
- Create abstractions where patterns emerge
- Reuse existing components

**SOLID Principles:**

- Single Responsibility
- Open/Closed (open for extension, closed for modification)
- Liskov Substitution
- Interface Segregation
- Dependency Inversion

**Testing:**

- Design for testability
- Clear test boundaries
- Mockable dependencies

**Developer Experience:**

- Clear, intuitive APIs
- Good error messages
- Minimal cognitive load
- Self-documenting code structures

## Decision-Making Framework

When choosing between alternatives:

1. **Simplicity first** - Prefer the simplest solution that works
2. **Testability** - Prefer designs that are easy to test
3. **Maintainability** - Prefer designs that are easy to understand and modify
4. **Performance** - Optimize only where measurements show it matters
5. **Flexibility** - Prefer designs that can adapt to future needs without major rewrites

**Red flags to avoid:**

- Over-engineering
- Premature optimization
- Tight coupling
- Hidden dependencies
- Magic behavior
- Unclear ownership

## Output Format

Design document must be valid YAML with:

- Proper indentation (2 spaces per level)
- Multi-line strings using pipe (`|`) syntax for architecture section
- Lists using dash (`-`) syntax
- Nested structures for decisions and components
- Clear, concise content (no verbose prose)

**Example YAML structure:**

```yaml
meta:
  phase: 0
  name: "Foundation"
  created: "2025-12-08"

goal: "Set up project structure and basic utilities"

architecture: |
  This phase uses a layered architecture with three components:
  FileManager, ConfigParser, and Logger.

  Data flows from config files through ConfigParser to FileManager
  for setup, with Logger tracking all operations.

decisions:
  - choice: "Use YAML for config"
    rationale: "Human-readable, supports nested structures"
    alternatives:
      - option: "JSON"
        rejected: "Less readable, no comments"

components:
  - name: "FileManager"
    purpose: "Handle file operations"
    interface:
      - "create_dir(path: str) -> bool"
      - "write_file(path: str, content: str) -> None"
    dependencies: ["Logger"]

error_handling:
  - scenario: "Directory already exists"
    strategy: "Skip creation, log warning"

testing:
  unit: "Test each component method with mocks"
  integration: "Test full setup workflow end-to-end"
  edge_cases:
    - "Empty paths"
    - "Permission errors"
```

## Integration with Next Phase

After saving design document, output summary:

- Path to saved design document
- Key architectural decisions
- Ready for planning phase

## Remember

- Make informed decisions based on best practices
- Document rationale for major decisions
- Consider future maintainability
- Optimize for clarity and simplicity
- Create designs that enable great implementation plans
