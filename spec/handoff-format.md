# Handoff Format Specification v1.0

## Abstract

This document specifies the structure and content of session handoff prompts in the LLM Project Templates system.

## Status

This is a living specification. Version 1.0 represents the initial standardisation effort.

## Purpose

A handoff format provides:
- Consistent structure across sessions
- Complete context transfer
- Self-contained continuation
- Pattern perpetuation

## Requirements

### MUST Requirements

A conforming handoff prompt MUST:

1. **Be self-contained**: Include all context necessary to continue work
2. **Reference the bootstrap template**: Ensure pattern continues
3. **Specify next objective**: Provide clear direction for next session
4. **Include continuation instructions**: Tell LLM to maintain the pattern
5. **Be valid markdown**: Parseable and renderable

### SHOULD Requirements

A conforming handoff prompt SHOULD:

1. **Summarize previous work**: List key accomplishments
2. **Document decisions**: Capture important choices with rationale
3. **Include timestamp**: Show when handoff was generated
4. **Version or number sessions**: Track progression
5. **Reference artifacts**: Link to created content
6. **Be concise**: Avoid unnecessary verbosity

### MAY Requirements

A conforming handoff prompt MAY:

1. **Include metadata**: Platform, model version, etc.
2. **Add domain-specific sections**: Research sources, code modules, etc.
3. **Provide alternative next steps**: Suggest multiple directions
4. **Include warnings or notes**: Flag potential issues
5. **Reference external resources**: Link to docs, tickets, etc.

## Standard Format

### Minimal Conformant Format

```markdown
=== SESSION HANDOFF ===

## Previous Session
[What was accomplished]

## Current State
[Where things stand]

## Next Objective
[What to do next]

## PROMPT FOR NEXT SESSION

Read and apply this bootstrap template:
[TEMPLATE_URL]

[Context and instructions for next session]

Remember: Say "[TRIGGER]" to generate the next handoff.
```

### Recommended Format

```markdown
=== SESSION HANDOFF ===
Generated: [ISO 8601 datetime]
Session: [identifier]

## Previous Session Summary

### Accomplished
- [Achievement 1]
- [Achievement 2]
- [Achievement 3]

### Decisions Made
- [Decision 1]: [Rationale]
- [Decision 2]: [Rationale]

### Artifacts Created
- [Artifact 1]: [Description]
- [Artifact 2]: [Description]

## Current Project State

[2-4 sentence summary of where the project stands]

## Next Session Objective

[Clear, specific goal for the next session]

## Context for Next Session

[Any additional context, constraints, or background needed]

---

## PROMPT FOR NEXT SESSION

Copy everything below this line into a new chat:

---

Read and apply this bootstrap template:
[TEMPLATE_URL]

## Project Context

[Brief project description and background]

## Work Completed So Far

[Summary of accomplishments from above]

## Current Status

[State description from above]

## This Session's Goal

[Next objective from above]

## Continue From

[References to artifacts, decisions, or specific starting points]

---

Remember: At session end, say "[TRIGGER]" to generate the next prompt.
```

## Section Specifications

### Header

**Purpose**: Identify this as a handoff and provide metadata

**Format**:
```markdown
=== SESSION HANDOFF ===
Generated: YYYY-MM-DDTHH:MM:SSZ
Session: <identifier>
```

**Fields**:
- `Generated`: ISO 8601 timestamp (SHOULD)
- `Session`: Session identifier, e.g., "Session 3 → 4" or "v1.2" (SHOULD)

### Previous Session Summary

**Purpose**: Capture what was accomplished

**Subsections**:
- **Accomplished**: Bullet list of achievements (SHOULD)
- **Decisions Made**: Bullet list of decisions with brief rationale (SHOULD)
- **Artifacts Created**: List of created content with descriptions (MAY)

**Guidelines**:
- Focus on outcomes, not process
- Include enough detail to reconstruct reasoning
- Maximum 5-7 items per subsection
- Use past tense

### Current Project State

**Purpose**: Describe where things stand now

**Format**: 2-4 sentence prose summary

**Should include**:
- Overall project progress
- What's working well
- What needs attention
- Blockers if any

**Example**:
```markdown
The authentication system is now complete and tested. API endpoints 
are functional with JWT token handling. Ready to begin work on the 
user profile management feature. No blockers currently.
```

### Next Session Objective

**Purpose**: Provide clear direction for continuation

**Format**: Single clear statement of what the next session should accomplish

**Should be**:
- Specific and actionable
- Achievable in one session
- Aligned with overall project goals

**Examples**:
```markdown
✓ Good: "Implement password reset functionality with email verification"
✗ Too vague: "Work on user features"
✗ Too broad: "Complete entire user management system"
```

### Context for Next Session

**Purpose**: Provide any additional background needed

**May include**:
- Technical constraints
- Dependencies
- Relevant resources
- Open questions
- Warnings or gotchas

**Format**: Prose or bullet list

### Restoration Prompt

**Purpose**: Complete, self-contained prompt for next session

**Must include**:
- Bootstrap template URL
- Project context
- Current state
- Next objective
- Continuation trigger instruction

**Should be**:
- Copy-pasteable without modification
- Completely self-contained
- Clear and unambiguous

## Domain-Specific Extensions

Implementations MAY add domain-specific sections:

### Research Projects
```markdown
### Sources Consulted
- [Citation 1]
- [Citation 2]

### Open Questions
- [Question 1]
- [Question 2]
```

### Software Development
```markdown
### Code Modules Modified
- [Module 1]: [Changes]
- [Module 2]: [Changes]

### Tests Added
- [Test 1]
- [Test 2]

### Technical Debt
- [Debt item 1]
- [Debt item 2]
```

### Content Creation
```markdown
### Content Pieces
- [Piece 1]: [Status]
- [Piece 2]: [Status]

### Editorial Decisions
- [Decision 1]
- [Decision 2]

### Review Status
[Current review state]
```

## Format Validation

A handoff can be validated against these criteria:

**Structural Validation**:
- [ ] Contains header section
- [ ] Contains previous session summary
- [ ] Contains current state
- [ ] Contains next objective
- [ ] Contains restoration prompt
- [ ] Restoration prompt includes template URL
- [ ] Restoration prompt includes continuation trigger

**Content Validation**:
- [ ] Previous session summary is specific
- [ ] Decisions include rationale
- [ ] Next objective is clear and actionable
- [ ] Restoration prompt is self-contained
- [ ] Total length is reasonable (not excessive)

**Format Validation**:
- [ ] Valid markdown
- [ ] Consistent heading levels
- [ ] No broken internal references
- [ ] Proper list formatting

## Examples

### Minimal Example

```markdown
=== SESSION HANDOFF ===

## Previous Session
Set up project structure and dependencies.

## Current State
Ready to begin implementation.

## Next Objective
Implement core data models.

## PROMPT FOR NEXT SESSION

Read and apply: https://example.com/templates/base.md

Project: Task management app
Status: Project setup complete
Goal: Implement User and Task models

Remember: Say "snapshot" to generate next handoff.
```

### Complete Example

```markdown
=== SESSION HANDOFF ===
Generated: 2025-10-05T14:30:00Z
Session: Session 2 → 3

## Previous Session Summary

### Accomplished
- Designed database schema with three main tables
- Set up SQLAlchemy models for User and Task
- Created initial migration scripts
- Configured pytest with fixtures

### Decisions Made
- PostgreSQL over SQLite: Better production scalability
- UUID primary keys: Enables distributed systems later
- Soft deletes: Preserve data for audit trail

### Artifacts Created
- models.py: User, Task, and Tag models
- test_models.py: Unit tests for model validation
- migration_001.sql: Initial schema

## Current Project State

The data layer is complete with tested models and migrations. Database 
schema supports all planned features including user authentication, task 
management, and tagging. Ready to build the API layer on this foundation.

## Next Session Objective

Implement REST API endpoints for user authentication (register, login, 
logout) with JWT tokens and proper error handling.

## Context for Next Session

Use FastAPI framework as decided in Session 1. Follow the authentication 
pattern from the team's standard template. Ensure all endpoints have 
comprehensive tests before considering complete.

---

## PROMPT FOR NEXT SESSION

Copy everything below this line:

---

Read and apply this bootstrap template:
https://raw.githubusercontent.com/example/templates/main/dev-base.md

## Project Context

Building a task management API with FastAPI and PostgreSQL. Following 
microservices architecture principles with emphasis on testing.

## Work Completed

- Session 1: Project setup, dependencies, CI/CD
- Session 2: Database models, schema, migrations, model tests

## Current Status

Data layer complete and tested. Database schema supports user auth, 
task CRUD, and tagging. All models have unit test coverage.

## This Session's Goal

Implement authentication API endpoints:
- POST /auth/register: User registration
- POST /auth/login: Login with JWT generation
- POST /auth/logout: Token invalidation
- Include request validation and error handling
- Full test coverage for all endpoints

## Technical Notes

- Use pyjwt for token generation
- Token expiry: 24 hours
- Password hashing: bcrypt
- Follow existing code style in models.py

---

Remember: Say "snapshot" when ready for the next handoff.
```

## Versioning

This specification uses semantic versioning:

- **Major**: Breaking changes to required format
- **Minor**: New optional sections or fields
- **Patch**: Clarifications, typo fixes

Current version: 1.0.0

## See Also

- [Session Handoff Pattern](../docs/patterns/session-handoff.md)
- [Bootstrap Pattern](../docs/patterns/bootstrap.md)
- [Implementation Guide](../docs/implementation-guide.md)