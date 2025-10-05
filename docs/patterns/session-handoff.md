# Session Handoff Pattern

## Intent

Structure LLM interactions as a chain of discrete sessions where each session generates the initialization prompt for its successor, enabling context continuity without indefinitely long conversations.

## Also Known As

- Prompt chaining
- Context propagation
- Session continuation pattern

## Motivation

Working on complex projects with LLMs presents several challenges:

1. **Context accumulation**: Long conversations become unwieldy and may degrade in quality
2. **Session boundaries**: Starting fresh sessions loses valuable context
3. **Decision tracking**: Difficult to identify key decisions in long transcripts
4. **Experimentation**: Hard to try alternative approaches without losing progress

The Session Handoff pattern addresses these by treating each chat as a discrete unit that explicitly passes context to the next.

## Applicability

Use this pattern when:

- Projects span multiple work sessions
- You need to track decisions and progress
- Context limits are a concern
- You want the ability to rollback or branch
- Multiple people might work on the same project asynchronously

Don't use this pattern when:

- Working on simple, one-off queries
- All work fits comfortably in a single session
- Context passing overhead exceeds benefit

## Structure

```
┌─────────────┐
│  Session 1  │
│             │
│ - Receives  │
│   initial   │
│   prompt    │
│ - Does work │
│ - Generates │──┐
│   handoff   │  │
└─────────────┘  │
                 │
                 ▼
              ┌─────────────┐
              │  Session 2  │
              │             │
              │ - Receives  │
              │   handoff   │
              │ - Does work │
              │ - Generates │──┐
              │   handoff   │  │
              └─────────────┘  │
                               │
                               ▼
                            ┌─────────────┐
                            │  Session 3  │
                            │     ...     │
                            └─────────────┘
```

## Participants

### Session (Handler)
- Receives context via handoff prompt
- Performs designated work
- Generates handoff for next session

### Handoff (Context Package)
- Contains summary of completed work
- Includes key decisions and state
- Specifies next objectives
- Carries continuation instructions

### Bootstrap Template
- Defines handoff format
- Specifies trigger mechanism
- Includes pattern instructions

## Collaborations

1. User initiates Session N with handoff prompt from Session N-1
2. Session N performs work, accumulating context
3. User triggers handoff generation
4. Session N creates structured handoff including:
   - Summary of work done
   - Current state
   - Next objectives
   - Instructions for Session N+1
5. User copies handoff and uses it to initialize Session N+1
6. Pattern repeats

## Consequences

### Benefits

**Focused sessions**: Each chat has a clear scope and objective, reducing cognitive load.

**Clean rollback**: Failed sessions can be abandoned; simply restart from previous handoff.

**Explicit state**: Context is deliberately summarized rather than implicitly accumulated.

**Branching capability**: Can start multiple sessions from the same handoff to explore alternatives.

**Shareable context**: Handoffs can be shared with collaborators for async work.

**Version control friendly**: Handoffs are text that can be committed to git.

### Liabilities

**Manual overhead**: Requires copying prompts between sessions and triggering handoffs.

**Compression loss**: Summarizing risks losing nuance from previous sessions.

**Format discipline**: Requires adherence to handoff format for consistency.

**Learning curve**: Users must understand the pattern to use it effectively.

## Implementation

### Define Trigger Mechanism

Choose how users signal handoff generation:
```
- Keyword: "snapshot", "handoff"
- Symbol: "→"
- Structured command: "/handoff"
```

### Specify Handoff Format

Create a template for handoff prompts:
```markdown
## Previous Session Summary
[What was accomplished]

## Current State
[Where things stand]

## Next Objective
[What to do next]

## Context
[Relevant background]

## Continuation Instructions
[How to maintain the pattern]
```

### Bootstrap Template

Include in your bootstrap:
```markdown
When user says [TRIGGER], generate next session prompt using:
[HANDOFF FORMAT]

Ensure each generated prompt includes these handoff instructions.
```

### Usage Pattern

1. Start session with handoff prompt
2. Work normally
3. Trigger handoff at session end
4. Copy generated prompt
5. Start new session
6. Repeat

## Sample Code

### Basic Handoff Prompt Structure

```markdown
Read and apply this bootstrap template:
[TEMPLATE_URL]

## Session Context

Previous session accomplished:
- [Achievement 1]
- [Achievement 2]

Current project state:
[State description]

This session's goal:
[Specific objective]

---

Remember: Say "snapshot" at session end to generate the next handoff.
```

### Generated Handoff Example

```markdown
=== SESSION HANDOFF ===
Session 2 → 3

## Previous Session Summary
- Created initial project structure
- Defined core data models
- Set up testing framework

## Current State
Project skeleton is complete. Ready to implement first feature.

## Next Objective
Implement user authentication module with tests.

## PROMPT FOR NEXT SESSION

Read and apply this bootstrap template:
https://[...]/base.md

## Session Context

We've completed the project setup phase. The structure includes:
- models/ with User and Session models
- tests/ with pytest configuration
- Basic CI/CD pipeline

This session should focus on:
Implementing user authentication (register, login, logout) with 
full test coverage.

Technical constraints:
- Use JWT for tokens
- Hash passwords with bcrypt
- Follow existing code style

---

Remember: Say "snapshot" when ready for the next handoff.
```

## Known Uses

- Multi-day research projects
- Iterative software development
- Long-form content creation
- Collaborative LLM workflows
- Experimental work requiring branching

## Related Patterns

### Chain of Responsibility
Session Handoff is essentially Chain of Responsibility where each handler constructs its successor rather than having a pre-configured chain.

### Memento
Handoff prompts act as mementos, capturing state that can be restored by reusing the prompt.

### Command
Each handoff prompt can be viewed as a Command object encapsulating the context and instructions for the next session.

### Template Method
Bootstrap templates define the skeleton of the workflow, with specific projects filling in the details.

## See Also

- [Memento Pattern](https://en.wikipedia.org/wiki/Memento_pattern)
- [Chain of Responsibility](https://en.wikipedia.org/wiki/Chain-of-responsibility_pattern)
- [Snapshot Pattern](./snapshots.md)
- [Bootstrap Pattern](./bootstrap.md)