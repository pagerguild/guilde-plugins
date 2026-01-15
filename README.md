# guilde-plugins

A Claude Code plugin marketplace for workflow automation, TDD, code review, and development tools.

## Overview

This marketplace provides modular, single-purpose plugins that can be installed independently or combined as needed. Each plugin follows Claude Code plugin best practices with progressive disclosure and strong trigger phrases.

## Available Plugins

| Plugin | Description | Components |
|--------|-------------|------------|
| *Coming soon* | Plugins being migrated from guilde-lite | |

## Installation

### Add Marketplace

```bash
/plugin marketplace add pagerguild/guilde-plugins
```

### Install Individual Plugins

```bash
# List available plugins
/plugin list pagerguild/guilde-plugins

# Install a specific plugin
/plugin install <plugin-name>@pagerguild/guilde-plugins
```

### Local Development

For plugin development or testing:

```bash
# Clone the repository
git clone https://github.com/pagerguild/guilde-plugins.git

# Use plugins locally
claude --plugin-dir ./guilde-plugins/plugins/<plugin-name>
```

## Plugin Categories

### Workflow
- **conductor-workflows** - Track and phase management for development workflows
- **tdd-automation** - Test-driven development with red/green/refactor phases

### Code Quality
- **multi-agent-review** - Parallel code review with specialized agents
- **code-review-pipeline** - Multi-stage review workflow

### Development Agents
- **exploration-agents** - Codebase exploration and analysis
- **implementation-agents** - Backend, frontend, database development
- **spec-agents** - Specification building

### Tools
- **mise-tools** - Mise-first development environment management
- **context-preservation** - Session state and error recovery
- **diagram-generation** - Mermaid and C4 diagrams
- **release-research** - Changelog and release tracking
- **docs-sync** - Documentation synchronization

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
