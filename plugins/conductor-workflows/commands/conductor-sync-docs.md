---
description: Synchronize documentation with implementation state
argument-hint: "[all|track:ID|file:path] [--check|--generate]"
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "Task"]
---

# /conductor-sync-docs Command

Ensures documentation stays synchronized with implementation, updating READMEs, API docs, architecture diagrams, and changelogs.

## Documentation Hierarchy

```
docs/
├── README.md                 # Project overview
├── CHANGELOG.md              # Version history
├── ARCHITECTURE.md           # System architecture
├── tutorials/                # Step-by-step guides
│   └── *.md
└── [topic]/                  # Topic-specific docs
    └── *.md

conductor/
├── product.md                # Product definition
├── tech-stack.md             # Technology decisions
├── workflow.md               # Workflow conventions
└── tracks/
    └── TRACK-ID/
        ├── spec.md           # Track specification
        └── plan.md           # Implementation plan
```

## Usage

```
/conductor-sync-docs                    # Sync all documentation
/conductor-sync-docs track:MULTI-001    # Sync specific track docs
/conductor-sync-docs --check            # Check sync status only
/conductor-sync-docs --generate         # Generate missing docs
```

## Sync Process

```
┌─────────────────────────────────────────────────────────────────┐
│                    DOC SYNC PROCESS                              │
│                                                                   │
│  1. Inventory                                                     │
│     ┌───────────┐ ┌───────────┐ ┌───────────┐                   │
│     │   Code    │ │   Docs    │ │  Diagrams │                   │
│     │  Changes  │ │  Current  │ │  Current  │                   │
│     └───────────┘ └───────────┘ └───────────┘                   │
│            ↓                                                      │
│  2. Compare                                                       │
│     ┌─────────────────────────────────────────────┐              │
│     │  Identify stale documentation               │              │
│     │  Find missing documentation                 │              │
│     │  Detect broken links                        │              │
│     └─────────────────────────────────────────────┘              │
│            ↓                                                      │
│  3. Update                                                        │
│     ┌───────────┐ ┌───────────┐ ┌───────────┐                   │
│     │   README  │ │    API    │ │   Arch    │                   │
│     │   Update  │ │   Docs    │ │  Diagrams │                   │
│     └───────────┘ └───────────┘ └───────────┘                   │
│            ↓                                                      │
│  4. Verify                                                        │
│     ┌─────────────────────────────────────────────┐              │
│     │  Validate links                             │              │
│     │  Check completeness                         │              │
│     │  Report status                              │              │
│     └─────────────────────────────────────────────┘              │
└─────────────────────────────────────────────────────────────────┘
```

## Actions

### Inventory Phase

Scan for documentation needs:

1. **Code changes:** Recent changes via git diff
2. **Existing docs:** Find all markdown files
3. **Architecture diagrams:** Find mermaid/puml files

### Compare Phase

Identify sync needs:

| Check | Method |
|-------|--------|
| Stale README | Compare code features vs README sections |
| Missing API docs | Compare exported functions vs documentation |
| Outdated diagrams | Compare architecture vs diagram content |
| Broken links | Validate all markdown links |

### Update Phase

For each documentation type:

1. **README Updates:** Feature lists, installation, usage examples
2. **API Documentation:** Function signatures, OpenAPI specs
3. **Architecture Diagrams:** Component accuracy, data flow
4. **Track Documentation:** spec.md and plan.md progress

### Verify Phase

Validate documentation:
- Check links
- Check completeness
- Check freshness

## Related Commands

- `/conductor-setup` - Initialize conductor infrastructure
- `/conductor-status` - View all tracks and progress
- `/conductor-checkpoint` - Create checkpoint commits
