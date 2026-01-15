---
description: Display status of all tracks or a specific track with progress details
argument-hint: "[TRACK-ID] [summary|detailed|json]"
allowed-tools: ["Read", "Glob", "Grep"]
---

# /conductor-status Command

Displays status of implementation tracks with progress metrics and phase details.

## Usage

```
/conductor-status                    # Summary of all tracks
/conductor-status FEAT-001           # Detailed status of specific track
/conductor-status --format=detailed  # Detailed view of all tracks
```

## Output Formats

### Summary Format (default)

```
═══════════════════════════════════════════════════════════════════
CONDUCTOR STATUS
═══════════════════════════════════════════════════════════════════

Active Tracks (1)
─────────────────────────────────────────────────────────────────

[~] MULTI-001: Multi-Agent Workflow Architecture
    Priority: P0 | Phase: 9 of 12 | Progress: 76%
    ████████████████████░░░░░ 86/113 tasks

═══════════════════════════════════════════════════════════════════
Overall Progress: 76% | Active: 1 | Backlog: 0 | Completed: 0
═══════════════════════════════════════════════════════════════════
```

### Detailed Format

```
═══════════════════════════════════════════════════════════════════
TRACK: MULTI-001
═══════════════════════════════════════════════════════════════════

Title:    Multi-Agent Workflow Architecture
Status:   In Progress
Priority: P0 (Critical Path)

Progress: 76% (86/113 tasks)
──────────────────────────────────────
████████████████████░░░░░

Phase Progress
──────────────────────────────────────
✓ Phase 1: Foundation [710fa35]        11/11 ████████████
→ Phase 9: Conductor Commands           0/8 ░░░░░░░░░░░░
○ Phase 10: Skill Packaging             0/6 ░░░░░░░░░░░░
```

## Status Icons

| Icon | Meaning |
|------|--------|
| `✓` | Phase completed |
| `→` | Current phase (in progress) |
| `○` | Future phase (pending) |
| `!` | Blocked |
| `█` | Progress filled |
| `░` | Progress empty |

## Track Status Markers

| Marker | Meaning |
|--------|--------|
| `[ ]` | Not Started |
| `[~]` | In Progress |
| `[x]` | Completed |
| `[!]` | Blocked |
| `[-]` | Cancelled |

## Related Commands

- `/conductor-setup` - Initialize conductor infrastructure
- `/conductor-new-track` - Create a new track
- `/conductor-implement` - Work on track implementation
- `/conductor-checkpoint` - Create checkpoint commits
- `/conductor-sync-docs` - Synchronize documentation
