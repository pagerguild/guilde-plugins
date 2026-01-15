---
description: Create a checkpoint commit marking phase completion with plan updates
argument-hint: "TRACK-ID [phase-number]"
allowed-tools: ["Read", "Edit", "Bash(git:*)"]
---

# /conductor-checkpoint Command

Creates a checkpoint commit marking the completion of a track phase, updating the plan with the commit hash.

## Checkpoint Purpose

Checkpoints serve as:
1. **Recovery points:** Can restore to any completed phase
2. **Progress markers:** Track implementation history
3. **Context anchors:** Reference point for session handoffs
4. **Audit trail:** Document what was completed when

## Usage

```
/conductor-checkpoint MULTI-001        # Checkpoint current phase
/conductor-checkpoint MULTI-001 9      # Checkpoint specific phase
```

## Checkpoint Process

```
┌─────────────────────────────────────────────────────────────────┐
│                    CHECKPOINT PROCESS                            │
│                                                                   │
│  1. Verify Ready                                                  │
│     ┌───────────┐ ┌───────────┐ ┌───────────┐                   │
│     │  Tasks    │ │  Quality  │ │   Tests   │                   │
│     │ Complete  │ │   Gates   │ │   Pass    │                   │
│     └───────────┘ └───────────┘ └───────────┘                   │
│            ↓                                                      │
│  2. Update Plan                                                   │
│     ┌─────────────────────────────────────────────┐              │
│     │  Mark tasks [x] complete                     │              │
│     │  Update progress summary                     │              │
│     │  Set current phase to next                  │              │
│     └─────────────────────────────────────────────┘              │
│            ↓                                                      │
│  3. Create Commit                                                 │
│     ┌─────────────────────────────────────────────┐              │
│     │  git add -A                                  │              │
│     │  git commit -m "conductor(checkpoint):..."   │              │
│     └─────────────────────────────────────────────┘              │
│            ↓                                                      │
│  4. Record Checkpoint                                             │
│     ┌─────────────────────────────────────────────┐              │
│     │  Update plan.md with commit hash            │              │
│     │  Update tracks.md status                    │              │
│     └─────────────────────────────────────────────┘              │
└─────────────────────────────────────────────────────────────────┘
```

## Actions

### 1. Verify Readiness

Before creating checkpoint, verify:

1. **Tasks complete:** All tasks in phase marked `[x]`
2. **Quality gates pass:** All quality gates marked `[x]}`, tests passing, lint clean
3. **Changes staged:** All relevant changes in staging area

### 2. Update Plan

Edit `conductor/tracks/TRACK-ID/plan.md`:

1. Mark tasks complete
2. Mark quality gates complete
3. Update progress summary
4. Update current phase header

### 3. Create Commit

```bash
git add -A
git commit -m "conductor(checkpoint): Complete Phase X - [Phase Name]

Track: TRACK-ID
Phase: X - [Phase Name]

Completed tasks:
- Task 1
- Task 2

Quality gates passed:
- [x] Gate 1
- [x] Gate 2

Co-Authored-By: Claude <noreply@anthropic.com>"
```

### 4. Record Checkpoint

1. Get hash: `git rev-parse --short HEAD`
2. Update phase header: `## Phase X: [Name] [checkpoint: abc1234]`
3. Update tracks.md if needed

## Commit Message Format

```
conductor(checkpoint): Complete Phase X - [Phase Name]

Track: TRACK-ID
Phase: X - [Phase Name]

Completed tasks:
- [List of completed tasks]

Quality gates passed:
- [x] [Gate descriptions]

Co-Authored-By: Claude <noreply@anthropic.com>
```

## Recovery from Checkpoint

```bash
# View checkpoint history
git log --oneline --grep="conductor(checkpoint)"

# Restore to specific checkpoint
git checkout <checkpoint-hash>

# Create branch from checkpoint
git checkout -b recovery-phase-9 <checkpoint-hash>
```

## Related Commands

- `/conductor-setup` - Initialize conductor infrastructure
- `/conductor-new-track` - Create a new track
- `/conductor-implement` - Work on track implementation
- `/conductor-status` - View all tracks and progress
- `/conductor-sync-docs` - Synchronize documentation
