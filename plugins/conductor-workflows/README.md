# conductor-workflows

Slash commands for orchestrating multi-phase implementation workflows using the conductor pattern.

## Overview

The conductor pattern provides structured project management with:
- **Tracks** - Top-level work items (features, bugs, infrastructure)
- **Phases** - Stages of implementation within a track
- **Checkpoints** - Git commits marking phase completions
- **Progress tracking** - Visual progress with metrics

## Commands

| Command | Description |
|---------|-------------|
| `/conductor-setup` | Initialize conductor infrastructure |
| `/conductor-new-track` | Create a new implementation track |
| `/conductor-implement` | Work on track's current phase |
| `/conductor-checkpoint` | Create checkpoint commit |
| `/conductor-status` | View track progress |
| `/conductor-sync-docs` | Synchronize documentation |

## Installation

```bash
/plugin install conductor-workflows@pagerguild/guilde-plugins
```

## Quick Start

```bash
# Initialize conductor in your project
/conductor-setup

# Create a new track
/conductor-new-track FEAT-001 "User Authentication" P0

# Start implementation
/conductor-implement FEAT-001

# Check progress
/conductor-status FEAT-001

# Create checkpoint after phase completion
/conductor-checkpoint FEAT-001
```

## Directory Structure Created

```
conductor/
├── tracks.md            # Master track registry
├── product.md           # Product definition
├── tech-stack.md        # Technology decisions
├── workflow.md          # Workflow conventions
└── tracks/
    └── TRACK-XXX/
        ├── spec.md      # What to build
        └── plan.md      # How to build it
```

## Track Workflow

```
/conductor-setup
      ↓
/conductor-new-track
      ↓
/conductor-implement  ←─┐
      ↓                  │
/conductor-checkpoint ──┘ (repeat per phase)
      ↓
/conductor-status (anytime)
```

## License

MIT
