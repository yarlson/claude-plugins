---
name: roadmap-builder
description: Interactive roadmap creation through structured questioning, optimized for ephemeral execution
when_to_use: when user wants to create a new development roadmap
version: 3.0.0
---

# Roadmap Builder

Create execution-ready roadmap through one-question-at-a-time dialogue.

## Process

Ask questions one at a time. Use AskUserQuestion tool with clear options.

### Questions Sequence

**1. Project name?**

- Free text input
- Example: "Calculator CLI"

**2. Programming language?**

- Options: Python, Go, Rust, TypeScript, Java, Other
- If Other: ask for specific language

**3. Test command?**

- Show common options for selected language:
  - Python: `pytest tests/ -v`
  - Go: `go test ./... -race -cover`
  - Rust: `cargo test`
  - TypeScript: `npm test` or `jest`
  - Java: `mvn test` or `gradle test`
- Allow custom command

**4. Lint command?**

- Show common options for selected language:
  - Python: `ruff check .` or `pylint`
  - Go: `golangci-lint run ./...`
  - Rust: `cargo clippy --all-targets`
  - TypeScript: `eslint .`
  - Java: `mvn checkstyle:check`
- Allow custom command

**5. One-sentence project goal?**

- Free text input
- Example: "Build a command-line calculator with expression parsing"

**6. How many phases?**

- Options: 2, 3, 4, 5, 6, More than 6
- Recommend: 3-6 phases for most projects

**7-N. For each phase, ask:**

- **Phase name?** (e.g., "Foundation", "Core Feature", "Integration")
- **Phase goal?** (one sentence, what this phase accomplishes)
- **Success criteria?** (2-4 measurable outcomes)
  - Ask: "What are 2-4 things that must work when this phase is done?"
  - Examples: "Calculator.add() works", "Tests pass", "CLI parses input"

### Build Roadmap YAML

After gathering all info, create roadmap at:
`docs/roadmaps/[YYYY-MM-DD]-[project-name-slug]-roadmap.yml`

Format:

```yaml
proj:
  name: "[Project Name]"
  lang: "[Language]"
  test: "[Test Command]"
  lint: "[Lint Command]"
  goal: "[One-sentence goal]"

phases:
  - id: 0
    name: "[Phase Name]"
    goal: "[Phase goal]"
    success:
      - "[Success criterion 1]"
      - "[Success criterion 2]"
      - "[Success criterion 3]"

  - id: 1
    name: "[Phase Name]"
    goal: "[Phase goal]"
    success:
      - "[Success criterion 1]"
      - "[Success criterion 2]"
```

### Validate Roadmap

Check:

- All required fields present
- Phase IDs sequential (0, 1, 2, ...)
- Each phase has 2-4 success criteria
- Valid YAML syntax

### Output

Display:

```
✅ Roadmap created: docs/roadmaps/[filename]

Project: [name]
Language: [lang]
Phases: [count]

To execute:
/autonomous-dev docs/roadmaps/[filename]

To review first:
cat docs/roadmaps/[filename]
```

## Tips for Good Roadmaps

**Phase granularity:**

- Each phase: 2-8 hours of work
- Too small: overhead of phase management
- Too large: hard to review, risky

**Success criteria:**

- Specific and measurable
- Testable (can verify with command)
- Clear definition of done

**Phase sequencing:**

- Foundation first (structure, utilities)
- Core features next (main functionality)
- Integration/polish last (CLI, API, docs)

**Examples:**

Good success criteria:

- "Calculator.add() returns correct sum"
- "Parser handles nested parentheses"
- "CLI prints result to stdout"

Bad success criteria:

- "Code is good" (not measurable)
- "Everything works" (not specific)
- "Ready for production" (ambiguous)
