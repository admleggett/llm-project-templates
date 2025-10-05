# Snapshot Pattern

## Intent

Capture and externalize the complete state of an LLM conversation at a point in time, enabling rollback, branching, and state restoration.

## Also Known As

- Memento
- Checkpoint
- Savepoint

## Motivation

When working iteratively with LLMs, you often need to:

- Try different approaches without losing progress
- Recover from failed sessions
- Share exact context with collaborators
- Track decision history
- Branch to explore alternatives

The Snapshot pattern enables these by capturing conversation state in a restorable format.

## Applicability

Use snapshots when:

- Experimental work might need rollback
- Multiple approaches should be tried
- Context needs to be shared
- Project history should be tracked
- Branching workflows are valuable

## Structure

```
┌──────────────────┐
│   Originator     │
│  (LLM Session)   │
│                  │
│  + createSnapshot()  ────────►  ┌──────────────┐
│  + restore(snap) ◄───────────── │   Snapshot   │
│                  │               │              │
└──────────────────┘               │  - context   │
                                   │  - decisions │
                                   │  - state     │
        │                          │  - timestamp │
        │                          └──────────────┘
        ▼
┌──────────────────┐
│   Caretaker      │
│  (User/Git)      │
│                  │
│  + save()        │
│  + load()        │
│  + list()        │
└──────────────────┘
```

## Participants

### Originator (LLM Session)
- Creates snapshot of current state
- Restores from snapshot when given one
- Has internal state that needs preservation

### Snapshot (Handoff Prompt)
- Stores state of the originator
- Immutable once created
- Self-contained and portable

### Caretaker (User/Version Control)
- Requests snapshot creation
- Stores snapshots
- Decides when to restore
- Never modifies snapshot contents

## Collaborations

1. Caretaker requests snapshot from Originator
2. Originator packages its state into a Snapshot
3. Caretaker stores the Snapshot (in git, filesystem, etc.)
4. When rollback needed, Caretaker provides Snapshot to new Originator instance
5. New Originator initializes from Snapshot state

## Consequences

### Benefits

**Rollback capability**: Can return to any previous state by reusing a snapshot.

**Branching**: Multiple sessions can start from the same snapshot, enabling parallel exploration.

**Shareability**: Snapshots are self-contained prompts that can be shared with others.

**History tracking**: Series of snapshots forms a project timeline.

**Version control**: Text-based snapshots work naturally with git.

### Liabilities

**Storage overhead**: Each snapshot duplicates some context.

**Manual management**: User must decide when to create and which to keep.

**Compression**: Snapshots necessarily compress/summarize the full conversation.

**No automatic restoration**: Platform doesn't automatically apply snapshots; user must manually paste.

## Implementation

### Snapshot Format

Define a consistent structure:

```markdown
=== SNAPSHOT ===
Timestamp: [ISO 8601 datetime]
Session: [identifier]
Version: [number or tag]

## Context
[Summarized background and decisions]

## Current State
[Where things stand now]

## Next Steps
[What should happen next]

## Restoration Prompt
[Complete prompt for new session]
```

### Creation Trigger

Specify how snapshots are created:
```
User says: "snapshot", "save", "checkpoint"
LLM generates: structured snapshot in defined format
```

### Storage Strategy

Options for snapshot storage:

**Local files**:
```bash
project/
  snapshots/
    session-01.md
    session-02.md
    session-03.md
```

**Git repository**:
```bash
git add snapshots/session-03.md
git commit -m "Snapshot: Completed data model design"
git tag v0.3
```

**Inline documentation**:
```markdown
# Project Log

## Session 3 (2025-10-05)
[snapshot content]

## Session 2 (2025-10-04)
[snapshot content]
```

### Restoration Process

1. Identify snapshot to restore from
2. Copy restoration prompt from snapshot
3. Start new LLM session
4. Paste prompt
5. Continue from that state

## Sample Code

### Snapshot Creation

```markdown
When user says "snapshot":

1. Generate snapshot using this format:

=== SNAPSHOT v[N] ===
Created: [current datetime]

## Previous Work
- [Achievement 1]
- [Achievement 2]

## Decisions Made
- [Decision 1 with rationale]
- [Decision 2 with rationale]

## Current State
[2-3 sentence summary]

## Next Objective
[Clear goal for next session]

## RESTORATION PROMPT
---
Copy below this line to restore this state:

[Complete, self-contained prompt including all context]
---
```

### Using a Snapshot

```markdown
# User copies the restoration prompt from a snapshot
# User starts new LLM session
# User pastes:

Read and apply this bootstrap template:
[template URL]

## Restoring from Snapshot v3

Project context:
[context from snapshot]

Work completed so far:
- [accomplishments]

Current state:
[state description]

Continue with:
[next objective]
```

### Snapshot Comparison

```markdown
# Comparing two snapshots to see what changed:

Snapshot v2 → v3 changes:
- Added: User authentication module
- Decided: Use JWT instead of sessions
- Completed: Login/logout endpoints
- Next: Implement password reset
```

## Known Uses

### Research Projects
- Snapshot after each major finding
- Branch to explore alternative hypotheses
- Rollback if approach proves unfruitful

### Software Development
- Snapshot after completing each feature
- Branch to try different implementations
- Tag releases with snapshots

### Content Creation
- Snapshot after each draft revision
- Try different narrative directions
- Preserve successful versions

### Collaborative Work
- Share snapshots with team members
- Team members continue from shared state
- Merge different branches manually

## Variants

### Lightweight Snapshots
Minimal state capture for simple workflows:
```markdown
v3: Completed auth module. Next: password reset.
```

### Rich Snapshots
Comprehensive state for complex projects:
```markdown
[Full context, all decisions, detailed state, artifacts, references]
```

### Differential Snapshots
Only capture changes from previous snapshot:
```markdown
Since v2:
- Added: [new elements]
- Changed: [modifications]
- Removed: [deletions]
```

### Tagged Snapshots
Meaningful labels instead of version numbers:
```markdown
- "baseline": Initial project state
- "mvp-complete": Minimum viable product done
- "pre-refactor": Before major restructure
```

## Related Patterns

### Command
Snapshots can be viewed as commands that initialize a session with specific state.

### Memento (original GoF)
This is essentially the Memento pattern applied to LLM conversations.

### Session Handoff
Handoff prompts are a special case of snapshots - snapshots with continuation instructions.

## Tips

### When to Snapshot

**Natural breakpoints**:
- End of work session
- After completing a milestone
- Before major direction changes
- When context feels "complete"

**Risk management**:
- Before trying experimental approaches
- When unsure about next steps
- After particularly successful sessions

### What to Include

**Essential**:
- Key decisions and rationale
- Current state/progress
- Next objectives

**Optional but valuable**:
- Timestamps
- Session identifiers
- References to artifacts
- Links to external resources
- Lessons learned

### What to Exclude

- Verbose conversation history
- Exploratory dead ends
- Redundant information
- Implementation details that can be regenerated

### Naming Conventions

```
session-01-initial-setup.md
session-02-data-modeling.md
session-03-auth-implementation.md

Or:

v1.0-baseline.md
v1.1-add-user-model.md
v2.0-auth-complete.md
```

## See Also

- [Session Handoff Pattern](./session-handoff.md)
- [Bootstrap Pattern](./bootstrap.md)
- [Memento Pattern (GoF)](https://en.wikipedia.org/wiki/Memento_pattern)