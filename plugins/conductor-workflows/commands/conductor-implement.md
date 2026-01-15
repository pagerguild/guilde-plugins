---
description: Work on implementing a track's current phase with guided workflow
argument-hint: TRACK-ID [phase-number]
allowed-tools: ["Read", "Write", "Edit", "Bash", "Task", "TodoWrite", "Glob", "Grep"]
---

# /conductor-implement Command

Guides implementation of a track's current phase with task tracking, TDD enforcement, and checkpoint creation.

## Workflow Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                    CONDUCTOR IMPLEMENT WORKFLOW                   │
│                                                                   │
│  1. Load Context                                                  │
│     ┌───────────┐ ┌───────────┐ ┌───────────┐                   │
│     │  spec.md  │ │  plan.md  │ │ tech-stack│                   │
│     └───────────┘ └───────────┘ └───────────┘                   │
│            ↓                                                      │
│  2. Phase Tasks                                                   │
│     ┌─────────────────────────────────────────────┐              │
│     │  [ ] Task 1 → [ ] Task 2 → [ ] Task 3       │              │
│     └─────────────────────────────────────────────┘              │
│            ↓                                                      │
│  3. TDD Loop (per task)                                          │
│     ┌──────────┐ ┌──────────┐ ┌──────────┐                      │
│     │   RED    │→│  GREEN   │→│ REFACTOR │                      │
│     └──────────┘ └──────────┘ └──────────┘                      │
│            ↓                                                      │
│  4. Quality Gates                                                 │
│     ┌───────────┐ ┌───────────┐ ┌───────────┐                   │
│     │   Tests   │ │   Lint    │ │  Review   │                   │
│     └───────────┘ └───────────┘ └───────────┘                   │
│            ↓                                                      │
│  5. Checkpoint                                                    │
│     ┌─────────────────────────────────────────────┐              │
│     │  git commit → update plan.md → next phase   │              │
│     └─────────────────────────────────────────────┘              │
└─────────────────────────────────────────────────────────────────┘
```

## Usage

```
/conductor-implement FEAT-001        # Work on current phase
/conductor-implement FEAT-001 3      # Work on specific phase
```

## Actions

### Load Context

When invoked, automatically read and understand:

1. **Track specification:** `conductor/tracks/TRACK-ID/spec.md`
2. **Implementation plan:** `conductor/tracks/TRACK-ID/plan.md`
3. **Technical context:** `conductor/tech-stack.md`

### Phase Execution

For each task in the current phase:

1. **Announce task:**
   ```
   Working on: [Task description]
   Phase: X of Y
   Task: N of M
   ```

2. **TDD workflow:**
   - RED: Write failing test first
   - GREEN: Implement minimal code to pass
   - REFACTOR: Clean up without changing behavior

3. **Track progress:**
   - Use TodoWrite for visibility
   - Update plan.md as tasks complete
   - Report blockers immediately

### Quality Gates

Before completing a phase, verify:

1. **Tests pass:** `task test`
2. **Linting clean:** `task lint`
3. **Coverage adequate:** `task test:coverage`
4. **Review complete:** Run `/review-all` for code review

### Checkpoint Creation

After phase completion:

1. **Stage changes:** `git add -A`
2. **Create checkpoint commit**
3. **Update plan.md** with checkpoint hash

## Related Commands

- `/conductor-setup` - Initialize conductor infrastructure
- `/conductor-new-track` - Create a new track
- `/conductor-status` - View all tracks and progress
- `/conductor-checkpoint` - Create checkpoint commits
- `/conductor-sync-docs` - Synchronize documentation
