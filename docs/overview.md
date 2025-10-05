# LLM Project Templates - Overview

## Core Concept

Instead of maintaining indefinitely long conversations with an LLM, this framework structures work as a series of connected sessions where each session generates the initialization prompt for the next.

## The Problem Space

### Context Window Limitations

Even with large context windows, very long conversations can:
- Become unwieldy and hard to navigate
- Degrade in quality as context accumulates
- Make it difficult to identify key decisions or progress

### Session Management Challenges

When working across multiple sessions:
- Context doesn't naturally carry forward
- You must manually summarize previous work
- There's no structured way to track progress
- Rolling back failed experiments is difficult

### Project Continuity

Complex projects need:
- Clear handoffs between work sessions
- Trackable decision history
- Ability to branch and experiment
- Version control over the conversation itself

## The Solution

### Session Handoff Pattern

Each chat session:
1. Receives context via a structured prompt
2. Performs its designated work
3. Generates a comprehensive prompt for the next session
4. Includes instructions to continue the pattern

This creates a **self-propagating chain** of sessions.

### Snapshot/Memento Approach

Each handoff prompt acts as a snapshot containing:
- Summary of completed work
- Key decisions made
- Current project state
- Next objectives
- Continuation instructions

These snapshots can be:
- **Reused**: Start a new session from any previous snapshot
- **Modified**: Edit before using to adjust direction
- **Versioned**: Store in git for project history
- **Shared**: Give collaborators the exact context you had

### Bootstrap Templates

Reusable templates define:
- Project initialization
- Workflow patterns
- Handoff formats
- Domain-specific structures

## How It Works in Practice

### Starting a Project

1. Choose or create a bootstrap template
2. Customize with your project specifics
3. Paste into new LLM chat
4. Begin work

### During a Session

- Work normally with the LLM
- Make decisions, create artifacts, solve problems
- Context accumulates naturally within the session

### Ending a Session

1. Say "snapshot" (or configured trigger word)
2. LLM generates next session prompt
3. Copy the generated prompt
4. Optionally: commit to version control

### Starting Next Session

1. Open new chat
2. Paste the generated prompt
3. Continue working
4. Repeat the cycle

### When Things Go Wrong

1. Delete the failed session
2. Use the previous snapshot prompt
3. Optionally: modify the prompt to avoid the same issue
4. Try again

## Design Patterns Used

### Chain of Responsibility

- Each session is a handler
- Handlers pass enriched context forward
- Each handler constructs its successor

### Memento

- Snapshots capture complete state
- State can be restored by reusing snapshots
- Enables rollback and branching

### Template Method

- Bootstrap templates define workflow skeleton
- Specific projects fill in the details
- Pattern remains consistent across projects

## Benefits

### For Individual Work

- **Focused sessions**: Each chat has a clear purpose
- **Clean context**: Start fresh without baggage
- **Easy rollback**: Undo failed experiments
- **Progress tracking**: Snapshots show evolution

### For Collaboration

- **Shareable state**: Hand off exact context to others
- **Async work**: Team members can continue from any snapshot
- **Documentation**: Handoff history serves as project log

### For Learning & Iteration

- **Experimentation**: Branch from any point
- **Pattern refinement**: Improve templates over time
- **Reproducibility**: Recreate workflows reliably

## Limitations & Considerations

### Manual Steps Required

- Copying prompts between sessions
- Triggering snapshot generation
- Deciding when to create new sessions

### Platform Dependency

- Implementation details vary by LLM
- Some features (like artifacts) are platform-specific
- May need adaptation for different models

### Learning Curve

- Requires understanding the pattern
- Initial setup more complex than ad-hoc chatting
- Best for substantial projects, not quick questions

## When to Use This Pattern

### Good Fit

- Multi-session projects (research, development, writing)
- Work requiring decision tracking
- Collaborative LLM projects
- Experimental work needing rollback capability
- Projects you'll return to over days/weeks

### Poor Fit

- Quick, one-off questions
- Simple tasks within a single session
- When immediate context is all you need

## Next Steps

- See [Implementation Guide](./implementation-guide.md) to adapt for your LLM
- Explore [Pattern Details](./patterns/) for deep dives
- Check [Examples](../examples/) for real workflows