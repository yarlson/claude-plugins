# Autonomous Development Flow Plugin

A Claude Code plugin that enables autonomous execution of multi-phase development roadmaps. Transform roadmap documents into fully implemented, tested features through automatic brainstorming, planning, and implementation phases—without user interaction.

## Overview

This plugin orchestrates three autonomous phases for each phase in your roadmap:

1. **Brainstorming** → Design document with architecture decisions
2. **Planning** → Detailed implementation plan with bite-sized tasks
3. **Implementation** → Working, tested code with quality gates

Perfect for executing well-defined roadmaps while maintaining high code quality and comprehensive documentation.

## Features

- ✅ **Autonomous Execution** - No user interaction needed during execution
- ✅ **Sequential Phase Management** - Phases execute one at a time in order
- ✅ **Quality Gates** - Enforces compilation, linting, and testing before commits
- ✅ **Test-Driven Development** - Strict TDD (RED-GREEN-REFACTOR) for all code
- ✅ **Comprehensive Documentation** - Generates design docs, plans, and reports
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

This interactive command will guide you through creating a comprehensive roadmap by asking questions about your project. It produces a roadmap optimized for autonomous execution.

**Or use the template:**
See `templates/roadmap-template.md` for a complete template you can fill in manually.

### Executing a Roadmap (Autonomous)

Once you have a roadmap:

```bash
/autonomous-dev path/to/roadmap.md
```

This will autonomously execute all phases: design → plan → implement for each phase.

### Roadmap Format

Your roadmap document should contain multiple phases with clear descriptions:

```markdown
# Project Roadmap

## Phase 0: Foundation

**Problem:** Need basic utilities and project structure

**Solution:** Create string utilities and directory structure

**Success Criteria:**

- Directory structure created
- String utilities working
- Tests passing

## Phase 1: Core Feature

**Problem:** Need to implement main feature logic

**Solution:** Implement tokenization and parsing

**Success Criteria:**

- Tokenizer working correctly
- Parser generates AST
- All tests passing

## Phase 2: Integration

...
```

The plugin will:

1. Read each phase
2. Create design document from phase requirements
3. Generate detailed implementation plan
4. Execute plan with quality gates
5. Move to next phase

### What Gets Generated

For each phase, the plugin creates:

```
docs/
├── designs/
│   └── YYYY-MM-DD-phase-N-<name>-design.md
├── plans/
│   └── YYYY-MM-DD-phase-N-<name>-plan.md
└── implementation-reports/
    └── YYYY-MM-DD-phase-N-<name>-report.md
```

Plus your implemented and tested code in the appropriate source directories.

## How It Works

### Phase Execution

For each phase in your roadmap:

#### 1. Autonomous Brainstorming

- Analyzes phase requirements
- Evaluates multiple architectural approaches
- Selects best approach based on:
  - Simplicity (YAGNI, DRY)
  - Maintainability
  - Testability
  - Developer experience
- Creates comprehensive design document

#### 2. Autonomous Planning

- Transforms design into detailed implementation plan
- Breaks down into bite-sized tasks (2-5 min each)
- Includes complete code examples
- Specifies exact file paths
- Adds TDD steps and verification

#### 3. Autonomous Implementation

- Executes plan task by task
- Dispatches fresh subagent per task
- Follows strict TDD: Write test → Verify fail → Implement → Verify pass
- Enforces quality gates before every commit:
  - ✅ Code compiles
  - ✅ Linter passes
  - ✅ All tests pass
  - ✅ No regressions
- Runs integration tests
- Generates implementation report

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
- Produces execution-ready roadmap
- Location: `commands/build-roadmap.md`

### 2. `/autonomous-dev` - Execute Roadmap

- Executes multi-phase roadmaps autonomously
- Runs brainstorming → planning → implementation for each phase
- Enforces quality gates
- Location: `commands/autonomous-dev.md`

## Skills Included

The plugin includes four skills:

### 1. Interactive Roadmap Builder

- Transforms rough ideas into structured roadmaps
- Interactive questioning and validation
- Optimizes roadmaps for autonomous execution
- Location: `skills/roadmap-builder/SKILL.md`

### 2. Autonomous Brainstorming

- Transforms requirements into designs
- Makes informed architecture decisions
- Documents design rationale
- Location: `skills/autonomous-brainstorming/SKILL.md`

### 3. Autonomous Planning

- Creates detailed implementation plans
- Breaks down into executable tasks
- Includes complete code examples
- Location: `skills/autonomous-planning/SKILL.md`

### 4. Autonomous Implementation

- Executes plans with subagents
- Enforces quality gates strictly
- Verifies integration thoroughly
- Location: `skills/autonomous-implementation/SKILL.md`

## Agents Included

### Autonomous Development Executor

- Orchestrates all three phases
- Manages sequential phase execution
- Makes technical decisions autonomously
- Location: `agents/autonomous-executor.md`

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

Roadmap: docs/plans/self-hosting-roadmap.md
Phases completed: 6/6

Documentation:
- 6 design documents in docs/designs/
- 6 implementation plans in docs/plans/
- 6 implementation reports in docs/implementation-reports/

Code changes:
- 47 commits
- 23 files created/modified
- 152 tests added (all passing)

Quality metrics:
- ✅ All code compiles
- ✅ Zero linter issues
- ✅ All tests passing
- ✅ No regressions
- ✅ Complete documentation

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
│   ├── autonomous-brainstorming/
│   │   └── SKILL.md
│   ├── autonomous-planning/
│   │   └── SKILL.md
│   └── autonomous-implementation/
│       └── SKILL.md
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

Test the plugin with a simple roadmap:

```bash
# Create test roadmap
cat > test-roadmap.md << 'EOF'
# Test Roadmap

## Phase 0: Simple Feature

**Problem:** Need a hello function

**Solution:** Implement hello() that returns "Hello, World!"

**Success Criteria:**
- Function exists
- Returns correct string
- Tests pass
EOF

# Run autonomous development
/autonomous-dev test-roadmap.md

# Verify output
ls -la docs/designs/
ls -la docs/plans/
ls -la docs/implementation-reports/
```

## License

MIT

## Author

Yaroslav K

## Version

1.0.0

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
