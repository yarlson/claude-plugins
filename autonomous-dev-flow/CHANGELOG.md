# Changelog

All notable changes to the Autonomous Development Flow plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.1] - 2025-11-19

### Changed

- **CRITICAL:** Clarified subagent-per-phase execution model - each phase MUST execute in its own separate subagent
- **CRITICAL:** Enforced zero user interaction - subagents are forbidden from asking questions
- Added explicit monitoring and restart mechanism for subagents that attempt to ask questions
- Updated main executor to dispatch fresh subagent for each phase (all 3 steps in one subagent)
- Added NO-QUESTIONS instruction to all phase subagent prompts
- Clarified that main agent orchestrates but doesn't execute phases directly

### Added

- Question detection and prevention mechanism in main executor
- Explicit decision-making guidelines for autonomous operation
- Visual diagrams showing correct vs incorrect execution patterns
- Completion verification checklist (subagents must check before reporting)
- List of 11 forbidden question patterns with examples
- Default decision guidance for common choice points
- Incomplete execution detection and restart mechanism
- Stronger restart prompt with "YOU WERE RESTARTED" warning
- Multi-level restart escalation (1st restart → 2nd restart with decision)

### Fixed

- Ambiguity about whether phases execute in subagents (now explicit: YES, mandatory)
- Potential for subagents to ask user questions (now forbidden with monitoring)
- Context pollution between phases (now prevented with fresh subagents)
- Resource management for large roadmaps (now handled with subagent-per-phase)

## [1.0.0] - 2025-11-19

### Added

- Initial release of Autonomous Development Flow plugin
- `/build-roadmap` command for interactive roadmap creation
- Autonomous Brainstorming skill for design generation
- Autonomous Planning skill for implementation plan creation
- Autonomous Implementation skill for code execution with quality gates
- Autonomous Development Executor agent for orchestration
- Interactive Roadmap Builder skill for roadmap creation
- `/autonomous-dev` command for roadmap execution
- `/build-roadmap` command for interactive roadmap building
- Support for multi-phase roadmap execution
- Sequential phase management (one phase at a time)
- Quality gates enforcement (compile, lint, test, no regressions)
- Test-driven development (TDD) workflow
- Language-agnostic support (Go, Python, Rust, TypeScript, Java, etc.)
- Comprehensive documentation generation (designs, plans, reports)
- Best practices enforcement (SOLID, DRY, YAGNI)
- Automatic subagent dispatch per task
- Integration verification after each phase
- Complete audit trail with commits and documentation

### Features

- Execute roadmaps autonomously without user interaction
- Transform phase requirements into designs automatically
- Generate detailed implementation plans with complete code examples
- Implement features with strict quality gates
- Verify compilation, linting, and testing before commits
- Follow RED-GREEN-REFACTOR TDD cycle
- Make informed technical decisions based on best practices
- Document design rationale and architecture decisions
- Create implementation reports with metrics
- Support for multiple programming languages
- Automatic language detection from project structure

### Documentation

- Comprehensive README with usage examples
- QUICKSTART guide for 5-minute setup
- ROADMAP-GUIDE for creating effective roadmaps
- Detailed skill documentation for all phases
- Agent documentation for orchestration
- Complete roadmap template
- Example roadmap (calculator project)
- Installation and verification scripts

### Quality Assurance

- Non-negotiable quality gates before commits
- Automatic retry mechanism for fixable failures
- Integration verification after phase completion
- Full test suite execution
- Lint and compilation checks
- No regression testing

## [Unreleased]

### Planned

- Support for parallel task execution within phases (when safe)
- Custom quality gate configuration
- Webhook notifications for phase completion
- Progress dashboard generation
- Rollback automation
- Performance benchmarking integration
- Security scanning integration
- Code coverage reporting
- Custom template support for design/plan documents
- Plugin configuration file support
- Multi-language project support (polyglot)
- Docker/container integration
- CI/CD pipeline integration
- Metrics and analytics dashboard

---

[1.0.0]: https://github.com/yourusername/autonomous-dev-flow/releases/tag/v1.0.0
