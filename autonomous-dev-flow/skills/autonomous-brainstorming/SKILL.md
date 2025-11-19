---
name: Autonomous Brainstorming
description: Transform rough requirements into fully-formed designs autonomously, making informed decisions based on best practices and DX principles
when_to_use: when you need to refine requirements into a design document without user interaction
version: 1.0.0
---

# Autonomous Brainstorming

## Overview

Transform requirements into fully-formed designs through autonomous analysis and decision-making, optimizing for best current and future developer experience (DX).

**Core principle:** Analyze requirements, explore alternatives internally, select the best approach, document comprehensively.

**Output:** A design document saved to `docs/designs/YYYY-MM-DD-<feature-name>-design.md`

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

Create comprehensive design document with:

**1. Overview**

- Problem statement
- Goals and non-goals
- Success criteria

**2. Architecture**

- High-level architecture (2-3 paragraphs)
- Key components and their responsibilities
- Data flow and interactions
- Technology choices and rationale

**3. Design Decisions**

- Major decisions made
- Alternatives considered and why rejected
- Trade-offs accepted

**4. Component Details**

- For each major component:
  - Purpose and responsibilities
  - Interfaces/APIs
  - Data structures
  - Dependencies

**5. Error Handling**

- Error scenarios
- Recovery strategies
- User-facing error messages

**6. Testing Strategy**

- Unit test approach
- Integration test approach
- Edge cases to cover

**7. Implementation Considerations**

- Potential challenges
- Areas needing special attention
- Dependencies on other systems

**8. Future Enhancements**

- Features intentionally deferred
- Extension points
- Migration considerations

### Phase 4: Save Design Document

Save to: `docs/designs/YYYY-MM-DD-<feature-name>-design.md`

Use clear, descriptive feature name (lowercase, hyphen-separated).

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

Design document should be:

- Clear and concise
- Well-structured with clear sections
- Detailed enough for implementation
- Including code examples where helpful
- Referencing existing patterns in the codebase

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
