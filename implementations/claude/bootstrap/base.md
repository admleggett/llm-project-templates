# Claude Project Bootstrap Template v1.0

## Workflow Pattern

This project uses an iterative session handoff pattern:

- Each session ends with a comprehensive prompt for the next chat
- Context, decisions, and progress carry forward automatically
- Failed sessions can be rolled back by reusing previous prompts
- Work is structured as a chain of connected sessions

## Session Handoff Instructions

When the user says **"snapshot"**, **"handoff"**, or **"→"**, generate the next session prompt using the format below.

## Snapshot Format

```
=== SESSION HANDOFF ===
Generated: [current date and time]
Session: [session number, e.g., "Session 3 → 4"]

## Previous Session Summary

### Accomplished
- [Key achievement 1]
- [Key achievement 2]
- [etc.]

### Decisions Made
- [Important decision 1]
- [Important decision 2]
- [etc.]

### Artifacts Created
- [Artifact 1: brief description]
- [Artifact 2: brief description]
- [etc.]

## Current Project State

[2-3 sentences describing where the project stands now]

## Next Session Objective

[Clear, specific goal for the next session]

## Context for Next Session

[Any additional context, constraints, or information needed]

---

## PROMPT FOR NEXT SESSION

Copy everything below this line into a new Claude chat:

---

Read and apply this bootstrap template:
https://raw.githubusercontent.com/YOUR-USERNAME/llm-project-templates/main/implementations/claude/bootstrap/base.md

## Project Context

[Include relevant context from above]

## Current Status

[Brief summary of project state]

## This Session's Goal

[The specific objective from above]

## Continue From

[Reference any artifacts or previous work]

---

Remember: At session end, say "snapshot" to generate the next prompt.
```

## Important Notes

- This template instructs Claude to continue the handoff pattern
- Each generated prompt is self-contained and includes the bootstrap URL
- The pattern perpetuates itself across sessions
- Users can break the chain anytime or customize the next prompt before using it

---

## Initial Task

[This section will be customized when you start a new project]