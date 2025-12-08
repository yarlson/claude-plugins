# Yarlson's Claude Code Plugins Marketplace

A curated collection of Claude Code plugins to enhance your development workflow.

## Overview

This repository serves as a plugin marketplace for Claude Code, providing easy access to custom plugins that extend Claude Code's capabilities with specialized tools and workflows.

**Marketplace Owner:** Yar Kravtsov (yarlson@gmail.com)

## Available Plugins

### Autonomous Development Flow

**Version:** 1.0.0
**Category:** Productivity
**License:** MIT

Autonomous multi-phase development workflow that executes roadmaps through brainstorming, planning, and implementation phases without user interaction.

**Features:**

- 🤖 **Autonomous Execution** - No user interaction during phases
- 📋 **Interactive Roadmap Builder** - `/build-roadmap` command guides you through roadmap creation
- 🎯 **Sequential Phase Management** - Execute phases one at a time with quality gates
- ✅ **Quality Gates** - Enforces compilation, linting, testing before commits
- 🧪 **Test-Driven Development** - Strict TDD (RED-GREEN-REFACTOR) workflow
- 📚 **Comprehensive Documentation** - Auto-generates designs, plans, and reports
- 🏗️ **Best Practices** - SOLID, DRY, YAGNI principles enforced automatically
- 🌐 **Language Agnostic** - Supports Go, Python, Rust, TypeScript, Java, and more

**Commands:**

- `/build-roadmap` - Interactive roadmap creation
- `/autonomous-dev <roadmap>` - Execute roadmap autonomously

**Documentation:**

- [Full README](./autonomous-dev-flow/README.md)
- [Quick Start Guide](./autonomous-dev-flow/QUICKSTART.md)
- [Roadmap Building Guide](./autonomous-dev-flow/ROADMAP-GUIDE.md)
- [Installation Guide](./autonomous-dev-flow/INSTALLATION.md)

### Agent Handoff Documentation

**Version:** 1.0.0
**Category:** Productivity
**License:** MIT

Generate comprehensive handoff documentation optimized for AI agent takeover. Zero configuration. Fully autonomous. Machine-readable first.

**Features:**

- 🤖 **Zero Configuration** - Works out of the box, no setup required
- ⚡ **Fully Autonomous** - No user questions during generation
- 🎯 **Adaptive Output** - Generates appropriate docs based on project type
- 📄 **8-Document Context Stack** - Complete handoff documentation suite
- 🔍 **Smart Project Detection** - Identifies libraries, services, CLI tools, monorepos
- 🌐 **Language Agnostic** - Supports Go, Python, TypeScript, Rust, Java, and more
- 📋 **Machine-Readable** - Optimized for AI agent consumption
- 🔄 **Git-Friendly** - All outputs are version-controllable text files

**Commands:**

- `/generate-handoff` - Generate complete handoff documentation

**What It Generates:**

- Handoff_Manifest.yaml (master index)
- PRD_Machine_Readable.md (requirements with Gherkin flows)
- Architecture_Decision_Records.md (design rationale)
- Domain_Dictionary.json (terminology mappings)
- System_Context_Map.mermaid (service boundaries)
- Agent_Runbook.md (build/test/deploy instructions)
- Codebase_Walkthrough_Annotated.md (directory guide)
- Test_Strategy_Matrix.md (quality gates)

**Documentation:**

- [Full README](./agent-handoff/README.md)

## Installation

### Quick Install

Add this marketplace to your Claude Code:

```bash
/plugin marketplace add yarlson/claude-plugins
```

Then install any plugin:

```bash
/plugin install autonomous-dev-flow@yarlson-claude-plugins
```

### Manual Installation

Clone this repository and install plugins directly:

```bash
# Clone the repository
git clone https://github.com/yarlson/claude-plugins.git
cd claude-plugins

# Install a specific plugin
cd autonomous-dev-flow
./install.sh
```

## Marketplace Structure

```
claude-plugins/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace configuration
├── autonomous-dev-flow/           # Plugin: Autonomous Development Flow
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   ├── agents/
│   ├── skills/
│   ├── templates/
│   ├── examples/
│   └── [documentation files]
└── README.md                      # This file
```

## Using the Marketplace

### Add the Marketplace

```bash
# Add from GitHub
/plugin marketplace add yarlson/claude-plugins

# Or add from local directory
/plugin marketplace add /path/to/claude-plugins

# Or add marketplace.json directly
/plugin marketplace add https://raw.githubusercontent.com/yarlson/claude-plugins/main/.claude-plugin/marketplace.json
```

### List Available Plugins

```bash
/plugin
```

This shows all plugins from all your configured marketplaces.

### Install a Plugin

```bash
# Install from this marketplace
/plugin install autonomous-dev-flow@yarlson-claude-plugins

# Or if it's the only marketplace with this plugin
/plugin install autonomous-dev-flow
```

### Update Plugins

```bash
# Update marketplace metadata
/plugin marketplace update yarlson-claude-plugins

# Update a specific plugin
/plugin update autonomous-dev-flow
```

### Remove Plugins

```bash
# Uninstall a plugin
/plugin uninstall autonomous-dev-flow

# Remove marketplace (also uninstalls all its plugins)
/plugin marketplace remove yarlson-claude-plugins
```

## For Teams

### Automatic Marketplace Installation

Add to your project's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "yarlson-plugins": {
      "source": {
        "source": "github",
        "repo": "yarlson/claude-plugins"
      }
    }
  },
  "enabledPlugins": {
    "autonomous-dev-flow": "yarlson-plugins"
  }
}
```

When team members trust the repository folder, Claude Code will:

1. Automatically install the marketplace
2. Automatically install specified plugins
3. Keep plugins synchronized across the team

## Plugin Development

### Adding a New Plugin

1. Create plugin directory:

   ```bash
   mkdir -p new-plugin/.claude-plugin
   cd new-plugin
   ```

2. Create `plugin.json`:

   ```json
   {
     "name": "new-plugin",
     "version": "1.0.0",
     "description": "Your plugin description",
     "author": {
       "name": "Your Name"
     }
   }
   ```

3. Add plugin components (commands, agents, skills, etc.)

4. Add to marketplace:
   Edit `.claude-plugin/marketplace.json`:

   ```json
   {
     "plugins": [
       {
         "name": "new-plugin",
         "source": "./new-plugin",
         "description": "Your plugin description",
         "version": "1.0.0"
       }
     ]
   }
   ```

5. Test locally:
   ```bash
   /plugin marketplace add /path/to/claude-plugins
   /plugin install new-plugin
   ```

### Plugin Guidelines

**Structure:**

- Use `.claude-plugin/plugin.json` for metadata
- Organize commands in `commands/`
- Organize agents in `agents/`
- Organize skills in `skills/`
- Include comprehensive README
- Provide examples

**Documentation:**

- Clear installation instructions
- Usage examples
- Troubleshooting section
- License information

**Quality:**

- Test all commands and features
- Validate JSON files
- Include examples
- Write clear documentation

## Marketplace Metadata

The marketplace is defined in `.claude-plugin/marketplace.json`:

```json
{
  "name": "yarlson-claude-plugins",
  "owner": {
    "name": "Yar Kravtsov",
    "email": "yarlson@gmail.com"
  },
  "metadata": {
    "description": "Claude Code plugins I made instead of yelling at my editor for the 400th time.",
    "version": "1.0.0"
  },
  "plugins": [
    {
      "name": "autonomous-dev-flow",
      "source": "./autonomous-dev-flow",
      "description": "...",
      "version": "1.0.0",
      "author": { "name": "Yaroslav K" },
      "license": "MIT",
      "keywords": [...],
      "category": "productivity"
    }
  ]
}
```

## Support

### Getting Help

**For plugin-specific issues:**

- Check the plugin's README
- Review the plugin's documentation
- Check the TROUBLESHOOTING section

**For marketplace issues:**

- Open an issue on GitHub
- Check Claude Code documentation

### Contributing

Contributions are welcome! To contribute:

1. Fork this repository
2. Create a feature branch
3. Add your plugin or improvements
4. Test thoroughly
5. Submit a pull request

**Guidelines:**

- Follow existing plugin structure
- Include comprehensive documentation
- Test all features
- Update marketplace.json
- Add examples

## Version History

### Marketplace Version 1.0.0 (2025-11-19)

**Added:**

- Initial marketplace setup
- Autonomous Development Flow plugin v1.0.0

## License

Each plugin has its own license. Check the plugin's LICENSE file for details.

- **Autonomous Development Flow**: MIT License

## Links

- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Plugin System Reference](https://docs.anthropic.com/claude-code/plugins)
- [Plugin Marketplaces Guide](https://docs.anthropic.com/claude-code/plugin-marketplaces)

---

**Note:** "Claude Code plugins I made instead of yelling at my editor for the 400th time."

---

Built with ❤️ for developers who value simplicity and speed.
