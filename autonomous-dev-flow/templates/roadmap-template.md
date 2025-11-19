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

- [Metric 1: How you measure success]
- [Metric 2: What good looks like]
- [Metric 3: Quality standards]

**Estimated Timeline:**

- Phase 0: [X hours]
- Phase 1: [Y hours]
- Phase 2: [Z hours]
- **Total:** [Sum] hours

---

## Phase 0: [Phase Name - Usually Foundation/Setup]

**Problem Statement:**
[Detailed description of what problem this phase solves. Be specific about the pain point or need.]

**Solution Overview:**
[High-level approach to solving the problem. What will be built and how will it work?]

**Success Criteria:**

- ✅ [Specific, measurable outcome 1]
- ✅ [Specific, measurable outcome 2]
- ✅ [Specific, measurable outcome 3]
- ✅ All tests passing
- ✅ Documentation updated

**Implementation Details:**

- [Key component 1: what it does]
- [Key component 2: what it does]
- [Technology/pattern to use: why this choice]
- [Edge case 1: how to handle]
- [Edge case 2: how to handle]

**Dependencies:**

- [None for Phase 0, or list prerequisites from external systems]

**Testing Strategy:**

- Unit tests: [What specific units to test]
- Integration tests: [What integrations to verify]
- Edge cases: [Specific scenarios to cover]

**Estimated Effort:** [X hours]

---

## Phase 1: [Phase Name]

**Problem Statement:**
[What problem this phase solves, building on Phase 0]

**Solution Overview:**
[High-level approach]

**Success Criteria:**

- ✅ [Specific outcome 1]
- ✅ [Specific outcome 2]
- ✅ [Specific outcome 3]
- ✅ All tests passing
- ✅ Integration with Phase 0 working

**Implementation Details:**

- [Component/feature 1]
- [Component/feature 2]
- [Important consideration 1]
- [Important consideration 2]

**Dependencies:**

- Requires Phase 0 complete
- [Any other dependencies]

**Testing Strategy:**

- Unit tests: [what to test]
- Integration tests: [what to verify]
- Edge cases: [scenarios]

**Estimated Effort:** [Y hours]

---

## Phase 2: [Phase Name]

[Same structure as above]

---

## Phase N: [Final Phase - Usually Documentation/Polish]

[Same structure as above]

---

## Testing Strategy (Overall)

**Unit Tests:**

- Approach: [How you'll structure unit tests]
- Coverage goal: [X%]
- Framework: [pytest, jest, go test, etc.]

**Integration Tests:**

- Approach: [How you'll test component interactions]
- Key scenarios: [List critical paths]

**End-to-End Tests:**

- [If applicable, describe full workflow tests]

**Performance Tests:**

- [If applicable, describe performance benchmarks]

---

## Quality Standards

**Code Quality:**

- Follow [PEP 8, JavaScript Standard Style, etc.]
- Use [type hints, JSDoc, etc.]
- Maximum function complexity: [cyclomatic complexity score]
- Code review: [Required? By whom?]

**Testing:**

- TDD approach (test first, then implement)
- Minimum coverage: [90%, 95%, etc.]
- All edge cases covered
- No flaky tests allowed

**Documentation:**

- API documentation for all public interfaces
- Usage examples for common scenarios
- Architecture overview document
- Contributing guide [if open source]
- Inline comments for complex logic

---

## Deliverables

After completing all phases, the project will include:

**Source Code:**

- [Component 1]: `src/path/to/component1`
- [Component 2]: `src/path/to/component2`
- [Component 3]: `src/path/to/component3`

**Tests:**

- [Test suite 1]: `tests/path/to/tests1`
- [Test suite 2]: `tests/path/to/tests2`

**Documentation:**

- README.md - Project overview and quick start
- docs/api.md - Complete API reference
- docs/architecture.md - System design and decisions
- docs/examples/ - Usage examples
- CHANGELOG.md - Version history

**Build Artifacts:**

- Package configuration (package.json, setup.py, Cargo.toml, etc.)
- Build scripts
- CI/CD configuration [if applicable]
- Deployment guides [if applicable]

---

## Risk Analysis

**High Priority Risks:**

- [Risk 1]: [Description and impact]
  - Mitigation: [How to prevent or handle]
  - Contingency: [What to do if it happens]

- [Risk 2]: [Description and impact]
  - Mitigation: [Strategy]
  - Contingency: [Backup plan]

**Medium Priority Risks:**

- [Risk 3]: [Description]
  - Mitigation: [Strategy]

**Low Priority Risks:**

- [Risk 4]: [Description]
  - Mitigation: [Strategy]

---

## Future Enhancements (Post-MVP)

Features intentionally deferred to keep initial scope manageable:

- [Feature 1]: [Description]
  - Reason for deferral: [Why not in MVP]
  - Estimated effort: [Hours/days]

- [Feature 2]: [Description]
  - Reason for deferral: [Why not in MVP]
  - Estimated effort: [Hours/days]

- [Feature 3]: [Description]
  - Reason for deferral: [Why not in MVP]
  - Estimated effort: [Hours/days]

---

## Notes

**Assumptions:**

- [Assumption 1 about environment, tools, or requirements]
- [Assumption 2]

**Constraints:**

- [Constraint 1: technical limitation or requirement]
- [Constraint 2]

**Open Questions:**

- [Question 1 that needs answering before or during implementation]
- [Question 2]

---

**Ready for autonomous execution with:**

```bash
/autonomous-dev docs/roadmaps/YYYY-MM-DD-[project-name]-roadmap.md
```

---

## How to Use This Template

1. **Replace all [placeholders]** with your actual content
2. **Keep all phases** following the same structure for consistency
3. **Be specific** in problem statements and success criteria
4. **Include testing** strategy for every phase
5. **Estimate time** realistically (each phase should be 2-8 hours)
6. **Document dependencies** between phases
7. **Think about edge cases** and error handling
8. **Consider the implementer** - assume zero codebase context

When complete, save to:
`docs/roadmaps/YYYY-MM-DD-[project-name]-roadmap.md`

Then execute with:
`/autonomous-dev docs/roadmaps/YYYY-MM-DD-[project-name]-roadmap.md`
