# Autonomous Development Flow Plugin

A Claude Code plugin that enables autonomous execution of multi-phase development roadmaps. Transform YAML roadmap documents into fully implemented, tested features through ephemeral execution with minimal handoffs—without user interaction.

## Overview

This plugin uses ephemeral execution for each phase in your roadmap:

1. **Think** (internal) → Architecture decisions not saved
2. **Plan** (internal) → Task breakdown not saved
3. **Implement** → Working, tested code with TDD
4. **Output** → Minimal handoff (50-100 tokens)

Perfect for executing well-defined roadmaps while achieving 90% token reduction through ephemeral thinking and minimal documentation.

## Features

- ✅ **Autonomous Execution** - No user interaction needed during execution
- ✅ **Sequential Phase Management** - Phases execute one at a time in order
- ✅ **Quality Gates** - Enforces compilation, linting, and testing before commits
- ✅ **Test-Driven Development** - Strict TDD (RED-GREEN-REFACTOR) for all code
- ✅ **Ephemeral Execution** - 90% token reduction via minimal handoffs
- ✅ **Code Review Integration** - Automated review after each phase (requires superpowers plugin)
- ✅ **Best Practices** - Applies SOLID, DRY, YAGNI principles automatically
- ✅ **Language Agnostic** - Supports Go, Python, Rust, TypeScript, Java, and more

## Installation

### From Local Directory

```bash
# Copy plugin to Claude Code plugins directory
cp -r autonomous-dev-flow ~/.claude/plugins/

# Or create symlink for development
ln -s /path/to/autonomous-dev-flow ~/.claude/plugins/autonomous-dev-flow
```

### Verify Installation

```bash
claude --debug
# Look for "Loading plugin: autonomous-dev-flow"
```

## Usage

### Creating a Roadmap (Interactive)

The easiest way to create an execution-ready roadmap:

```bash
/build-roadmap
```

This interactive command will guide you through creating a comprehensive roadmap by asking questions about your project. It produces a YAML roadmap optimized for autonomous execution.

**Or use the template:**
See `templates/roadmap-template.yml` for a complete template you can fill in manually.

### Executing a Roadmap (Autonomous)

Once you have a roadmap:

```bash
/autonomous-dev path/to/roadmap.yml
```

This will autonomously execute all phases: design → plan → implement for each phase.

### Roadmap Format

Your roadmap document should be in YAML format with project metadata and phases:

```yaml
proj:
  name: "Project Name"
  lang: "Python"
  test: "pytest tests/ -v"
  lint: "ruff check ."
  goal: "One sentence project objective"

phases:
  - id: 0
    name: "Foundation"
    goal: "Create basic utilities and project structure"
    success:
      - "Directory structure created"
      - "String utilities working"
      - "Tests passing"

  - id: 1
    name: "Core Feature"
    goal: "Implement tokenization and parsing"
    success:
      - "Tokenizer working correctly"
      - "Parser generates AST"
      - "All tests passing"

  - id: 2
    name: "Integration"
    goal: "Integrate with existing systems"
    success:
      - "Integration complete"
      - "All tests passing"
```

The plugin will:

1. Read each phase
2. Create design document from phase requirements
3. Generate detailed implementation plan
4. Execute plan with quality gates
5. Move to next phase

### What Gets Generated

For each phase:

```
docs/
├── handoffs/
│   └── phase-N-handoff.yml         # 50-100 tokens
└── implementation-reports/
    └── final-report.md               # Generated at end

src/                                   # Your actual code
tests/                                 # Your tests
```

Handoffs are minimal (50-100 tokens) and contain:
- Components created
- Key API signatures
- Architectural patterns used

Code is self-documenting. Tests document behavior.

## How It Works

### Phase Execution

For each phase:

1. **Execute Phase**
   - Think internally (architecture decisions)
   - Plan internally (task breakdown)
   - Implement with TDD (test → verify RED → impl → verify GREEN)
   - Output minimal handoff (50-100 tokens)

2. **Code Review**
   - Automated review with superpowers:code-reviewer
   - Fix issues if found (up to 3 review cycles)
   - Proceed only when approved

3. **Continue to Next Phase**
   - Next phase reads minimal handoff
   - Reads actual code for details
   - Builds on previous work

### Quality Gates (Non-Negotiable)

Before ANY commit:

1. ✅ **Code compiles** without errors
2. ✅ **Linter passes** with zero issues
3. ✅ **All tests pass** with zero failures
4. ✅ **No regressions** in existing functionality

The plugin **never commits** code that fails any quality gate.

## Configuration

### Language Detection

The plugin automatically detects your project language from:

- File extensions (`.go`, `.py`, `.rs`, `.ts`, etc.)
- Build files (`go.mod`, `package.json`, `Cargo.toml`, etc.)
- Project structure

### Language-Specific Commands

**Go:**

```bash
go build ./...                          # Compile
golangci-lint run --fix ./...           # Lint
go test ./... -race -cover              # Test
```

**Python:**

```bash
ruff check --fix . && mypy .           # Lint
pytest tests/ -v --cov                 # Test
```

**Rust:**

```bash
cargo build                             # Compile
cargo clippy --all-targets              # Lint
cargo test                              # Test
```

**TypeScript:**

```bash
eslint --fix . && tsc --noEmit         # Lint
npm test                                # Test
```

## Commands Included

### 1. `/build-roadmap` - Interactive Roadmap Builder

- Guides you through creating a roadmap
- Asks structured questions one at a time
- Validates incrementally
- Produces execution-ready YAML roadmap
- Location: `commands/build-roadmap.md`

### 2. `/autonomous-dev` - Execute Roadmap

- Executes multi-phase YAML roadmaps autonomously
- Runs brainstorming → planning → implementation for each phase
- Generates compact YAML designs and plans
- Enforces quality gates
- Location: `commands/autonomous-dev.md`

## Skills Included

The plugin includes two skills:

### 1. Roadmap Builder

- Transforms rough ideas into structured YAML roadmaps
- Interactive questioning and validation
- Optimizes roadmaps for autonomous execution
- Location: `skills/roadmap-builder/SKILL.md`

### 2. Autonomous Phase Execution

- Single unified skill for complete phase execution
- Internal thinking and planning (ephemeral)
- TDD implementation with quality gates
- Outputs minimal handoff documents
- Location: `skills/autonomous-phase-execution/SKILL.md`

## Agents Included

### Autonomous Development Executor

- Orchestrates phase execution with code review gates
- Manages sequential phase execution
- Integrates automated code review after each phase
- Handles review feedback loops
- Makes technical decisions autonomously
- Location: `agents/autonomous-executor.md`

### Code Review Integration

After each phase, automated code review runs (requires superpowers plugin):
- Reviews all code changes from phase
- Identifies architecture issues, missing tests, etc.
- Provides specific feedback
- Blocks next phase until issues resolved

If superpowers unavailable, review is skipped with warning.

## Best Practices Enforced

**Architecture:**

- SOLID principles
- Clean architecture
- Separation of concerns
- Single responsibility

**Code Quality:**

- DRY (Don't Repeat Yourself)
- YAGNI (You Aren't Gonna Need It)
- Test-driven development
- Clear, self-documenting code

**Process:**

- Small, focused commits
- Frequent integration
- Continuous verification
- Quality gates before commits

## Example Output

```
🎉 Autonomous Development Complete!

Roadmap: docs/roadmaps/calculator-cli-roadmap.yml
Phases completed: 3/3

Documentation:
- 3 handoff documents (YAML) in docs/handoffs/ (~250 tokens total)
- 1 final report (Markdown) in docs/implementation-reports/

Code changes:
- 12 commits
- 8 files created/modified
- 45 tests added (all passing)

Quality metrics:
- ✅ All code compiles
- ✅ Zero linter issues
- ✅ All tests passing
- ✅ No regressions
- ✅ All phases code reviewed

Token efficiency:
- ~90% reduction vs v1.0.0
- ~97% reduction in per-phase documentation
- Faster processing
- Lower API costs

Status: Ready for review and merge
```

## When to Use

**Perfect for:**

- Multi-phase feature roadmaps
- Well-defined requirements
- Projects needing comprehensive documentation
- Teams wanting consistent quality
- Long-running development sprints

**Not ideal for:**

- Exploratory prototyping
- Unclear requirements
- Need for human design input
- Parallel phase execution required
- Experimental features

## Limitations

**Does not:**

- Use git worktrees (works in current directory)
- Execute phases in parallel
- Skip quality gates for any reason
- Make breaking changes without planning
- Proceed with known issues

**Does:**

- Execute phases sequentially
- Enforce quality gates strictly
- Make informed technical decisions
- Follow industry best practices
- Document comprehensively
- Verify thoroughly at all levels

## Troubleshooting

### Plugin Not Loading

```bash
# Check plugin directory structure
ls -la ~/.claude/plugins/autonomous-dev-flow/

# Should show:
# .claude-plugin/plugin.json
# commands/autonomous-dev.md
# agents/autonomous-executor.md
# skills/*/SKILL.md
```

### Quality Gate Failures

The plugin will attempt to fix quality gate failures automatically (up to 3 attempts). If it cannot fix:

1. Check error messages in the output
2. Review the last commit
3. Run quality commands manually:

   ```bash
   # Compile
   [language-specific build command]

   # Lint
   [language-specific lint command]

   # Test
   [language-specific test command]
   ```

### Phase Blockers

If a phase cannot complete, the plugin will:

1. Report the specific blocker
2. Document what was completed
3. Stop execution (not proceed to next phase)
4. Provide diagnostic information

## Development

### Plugin Structure

```
autonomous-dev-flow/
├── .claude-plugin/
│   └── plugin.json              # Plugin metadata
├── commands/
│   └── autonomous-dev.md        # Slash command
├── agents/
│   └── autonomous-executor.md   # Main orchestration agent
├── skills/
│   ├── roadmap-builder/
│   │   └── SKILL.md
│   └── autonomous-phase-execution/
│       └── SKILL.md
├── templates/
│   └── roadmap-template.yml     # Roadmap template
└── README.md                    # This file
```

### Contributing

To contribute:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test with a sample roadmap
5. Submit a pull request

### Testing

Test the plugin with a simple YAML roadmap:

```bash
# Create test roadmap
cat > test-roadmap.yml << 'EOF'
proj:
  name: "Test Feature"
  lang: "Python"
  test: "pytest tests/ -v"
  lint: "ruff check ."
  goal: "Simple hello function"

phases:
  - id: 0
    name: "Simple Feature"
    goal: "Implement hello() that returns 'Hello, World!'"
    success:
      - "Function exists"
      - "Returns correct string"
      - "Tests pass"
EOF

# Run autonomous development
/autonomous-dev test-roadmap.yml

# Verify output
ls -la docs/handoffs/               # Minimal .yml files (~100 tokens each)
ls -la docs/implementation-reports/ # Final .md report
```

## License

MIT

## Author

Yaroslav K

## Version

3.0.0

## Keywords

autonomous, development, workflow, multi-phase, roadmap, TDD, quality-gates, best-practices

## Support

For issues and questions:

- Check the troubleshooting section above
- Review the skills documentation in `skills/*/SKILL.md`
- Check the agent documentation in `agents/autonomous-executor.md`

## Related

- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Plugin System](https://docs.anthropic.com/claude-code/plugins)
- [Slash Commands](https://docs.anthropic.com/claude-code/slash-commands)
- [Subagents](https://docs.anthropic.com/claude-code/sub-agents)

---

Built with ❤️ for developers who value simplicity and speed.
