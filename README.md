# guilde-plugins

A Claude Code plugin marketplace for workflow automation, TDD, code review, and development tools.

## Overview

This marketplace provides modular, single-purpose plugins that can be installed independently or combined as needed. Each plugin follows Claude Code plugin best practices with progressive disclosure and strong trigger phrases.

## Available Plugins

| Plugin | Description | Components |
|--------|-------------|------------|
| conductor-workflows | Track and phase management for development workflows | 6 commands |

## Installation

### Add Marketplace

```bash
claude plugin marketplace add github:pagerguild/guilde-plugins
```

### List Available Plugins

```bash
claude plugin marketplace list
```

### Install Individual Plugins

```bash
# Install a specific plugin
claude plugin install conductor-workflows@guilde-plugins

# Enable/disable plugins
claude plugin enable conductor-workflows@guilde-plugins
claude plugin disable conductor-workflows@guilde-plugins
```

### Validate Plugins

```bash
# Validate a local plugin or marketplace
claude plugin validate ./plugins/conductor-workflows
```

### Local Development

For plugin development or testing:

```bash
# Clone the repository
git clone https://github.com/pagerguild/guilde-plugins.git

# Use plugins locally (session only)
claude --plugin-dir ./guilde-plugins/plugins/conductor-workflows
```

## Plugin Categories

### Workflow
- **conductor-workflows** - Track and phase management for development workflows
- **tdd-automation** *(coming soon)* - Test-driven development with red/green/refactor phases

### Code Quality
- **multi-agent-review** *(coming soon)* - Parallel code review with specialized agents
- **code-review-pipeline** *(coming soon)* - Multi-stage review workflow

### Development Agents
- **exploration-agents** *(coming soon)* - Codebase exploration and analysis
- **implementation-agents** *(coming soon)* - Backend, frontend, database development
- **spec-agents** *(coming soon)* - Specification building

### Tools
- **mise-tools** *(coming soon)* - Mise-first development environment management
- **context-preservation** *(coming soon)* - Session state and error recovery
- **diagram-generation** *(coming soon)* - Mermaid and C4 diagrams
- **release-research** *(coming soon)* - Changelog and release tracking
- **docs-sync** *(coming soon)* - Documentation synchronization

## Plugin Structure

Each plugin follows this structure:

```
plugins/<plugin-name>/
├── README.md           # Plugin documentation
├── agents/             # Agent definitions (if any)
│   └── *.md
├── commands/           # Slash commands (if any)
│   └── *.md
└── skills/             # Skills with progressive disclosure (if any)
    └── <skill-name>/
        ├── SKILL.md
        ├── examples/
        └── references/
```

## CLI Reference

| Command | Description |
|---------|-------------|
| `claude plugin marketplace add <source>` | Add a marketplace |
| `claude plugin marketplace list` | List configured marketplaces |
| `claude plugin marketplace remove <name>` | Remove a marketplace |
| `claude plugin marketplace update [name]` | Update marketplace(s) |
| `claude plugin install <plugin>` | Install a plugin |
| `claude plugin uninstall <plugin>` | Uninstall a plugin |
| `claude plugin enable <plugin>` | Enable a plugin |
| `claude plugin disable <plugin>` | Disable a plugin |
| `claude plugin validate <path>` | Validate a plugin manifest |

## Contributing

1. Fork this repository
2. Create a new plugin in `plugins/<your-plugin-name>/`
3. Follow the [plugin structure](#plugin-structure) guidelines
4. Add your plugin to `.claude-plugin/marketplace.json`
5. Submit a pull request

## Related Projects

- [guilde-lite](https://github.com/pagerguild/guilde-lite) - The source project for these plugins
- [claude-plugins-official](https://github.com/anthropics/claude-plugins-official) - Anthropic's official plugin marketplace

## License

MIT License - See [LICENSE](LICENSE) for details.
