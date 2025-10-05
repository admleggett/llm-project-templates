# Bootstrap Template Schema v1.0

## Abstract

This document specifies the structure and requirements for bootstrap templates in the LLM Project Templates system.

## Status

This is a living specification. Version 1.0 represents the initial standardization effort.

## Purpose

Bootstrap templates initialize LLM sessions with:
- Workflow pattern instructions
- Handoff format specifications
- Trigger definitions
- Continuation mechanisms

## Requirements

### MUST Requirements

A conforming bootstrap template MUST:

1. **Define the workflow pattern**: Explain the session handoff concept
2. **Specify trigger mechanism**: Define how users request handoff generation
3. **Include handoff format**: Provide structure for generated prompts
4. **Ensure continuation**: Instruct LLM to include pattern in generated prompts
5. **Be accessible via URL**: Hosted where LLMs can fetch it
6. **Be valid markdown**: Properly formatted and parseable

### SHOULD Requirements

A conforming bootstrap template SHOULD:

1. **Include version number**: Track template evolution
2. **Provide examples**: Show what good handoffs look like
3. **Document customization points**: Guide project-specific adaptation
4. **Be self-contained**: Not require external dependencies
5. **Explain the why**: Help users understand the pattern

### MAY Requirements

A conforming bootstrap template MAY:

1. **Include domain-specific sections**: Tailor for research, development, etc.
2. **Define multiple triggers**: Support various commands
3. **Provide variations**: Offer format alternatives
4. **Include best practices**: Share tips and guidelines
5. **Reference related templates**: Link to specialized versions

## Standard Structure

### Minimal Conformant Template

```markdown
# [Template Name] v[Version]

## Workflow Pattern
[Explanation of session handoff pattern]

## Handoff Trigger
When user says "[TRIGGER]", generate next session prompt.

## Handoff Format
```
[Format specification]
```

Ensure generated prompts include:
- This template URL
- Instructions to continue pattern

## Initial Task
[Customization point for project start]
```

### Recommended Template Structure

```markdown
# [Template Name] v[Version]

## Overview
[Brief description of what this template does]

## Workflow Pattern
[Detailed explanation of session handoff approach]

## Session Handoff Instructions

When the user says **"[PRIMARY_TRIGGER]"** (or "[ALTERNATE_TRIGGER]"), 
generate the next session prompt using the format below.

## Handoff Format

```
[Complete format specification with all sections]
```

## Important Notes
[Key points about template usage]

## Example Handoff
[Complete example of a generated handoff]

## Customization Points

Fill in these sections for your specific project:
- [Point 1]
- [Point 2]
- [Point 3]

## Initial Task
[Placeholder for project-specific starting work]
```

## Section Specifications

### Header

**Purpose**: Identify template and version

**Format**:
```markdown
# [Template Name] v[Version]
```

**Requirements**:
- Template name SHOULD be descriptive
- Version MUST follow semantic versioning (major.minor.patch)
- First h1 heading in document

**Examples**:
```markdown
# Base Bootstrap Template v1.0
# Research Project Template v2.1
# Claude Bootstrap with Artifacts v1.0.2
```

### Overview

**Purpose**: Quickly orient users to template purpose

**Format**: 1-3 sentence description

**Should answer**:
- What is this template for?
- Who should use it?
- What patterns does it implement?

**Example**:
```markdown
## Overview

This template establishes an iterative session handoff workflow for 
software development projects. It's designed for multi-session coding 
tasks requiring context continuity and the ability to rollback failed 
experiments.
```

### Workflow Pattern

**Purpose**: Explain the session handoff concept

**Should describe**:
- How sessions chain together
- Why this approach is valuable
- What users should expect

**Format**: Prose explanation, optionally with bullet points

**Example**:
```markdown
## Workflow Pattern

This project uses an iterative session handoff pattern:

- Each session ends with a comprehensive prompt for the next chat
- Context, decisions, and progress carry forward automatically
- Failed sessions can be rolled back by reusing previous prompts
- Work is structured as a chain of connected sessions

This approach enables:
- Clean session boundaries without losing context
- Easy rollback when experiments fail
- Sharable project state via handoff prompts
- Version-controlled conversation history
```

### Handoff Trigger

**Purpose**: Define how users request handoff generation

**Must specify**:
- Primary trigger word/phrase
- Any alternate triggers (optional)
- What happens when triggered

**Format**:
```markdown
## Session Handoff Instructions

When the user says **"[TRIGGER]"**, generate the next session 
prompt using the format below.
```

**Common triggers**:
- "snapshot"
- "handoff"
- "→"
- "checkpoint"
- "/next"

**Example with alternates**:
```markdown
## Session Handoff Instructions

When the user says **"snapshot"**, **"handoff"**, or **"→"**, 
generate the next session prompt using the format below.
```

### Handoff Format

**Purpose**: Specify exact structure for generated prompts

**Must include**:
- All required sections
- Format for each section
- Instructions for continuation

**Format**: Code block or detailed specification

**Example**:
````markdown
## Handoff Format

```
=== SESSION HANDOFF ===
Generated: [current date and time]
Session: [session number]

## Previous Session Summary

### Accomplished
- [Key achievement 1]
- [Key achievement 2]

### Decisions Made
- [Decision 1 with rationale]
- [Decision 2 with rationale]

## Current Project State
[2-3 sentence summary]

## Next Session Objective
[Clear, specific goal]

---

## PROMPT FOR NEXT SESSION

Read and apply this bootstrap template:
[THIS_TEMPLATE_URL]

[Complete context and instructions for next session]

Remember: Say "[TRIGGER]" to generate the next prompt.
```
````

### Continuation Instructions

**Purpose**: Ensure pattern perpetuates across sessions

**Must specify**:
- Template URL must be included in generated prompts
- Pattern instructions must carry forward
- Trigger mechanism must be communicated

**Example**:
```markdown
## Important Notes

- This template instructs the LLM to continue the handoff pattern
- Each generated prompt is self-contained and includes the bootstrap URL
- The pattern perpetuates itself across sessions
- Users can break the chain anytime or customize prompts before using
```

### Example Handoff

**Purpose**: Show template users what good output looks like

**Should include**:
- Complete example of a generated handoff
- Real-looking content (not just placeholders)
- All sections properly formatted

**Format**: Full example in code block

**Example**:
````markdown
## Example Handoff

Here's what a handoff generated from this template looks like:

```
=== SESSION HANDOFF ===
Generated: 2025-10-05T14:30:00Z
Session: Session 2 → 3

## Previous Session Summary

### Accomplished
- Created initial React component structure
- Set up Tailwind CSS configuration
- Implemented basic navigation layout

### Decisions Made
- Next.js App Router over Pages Router: Better for modern patterns
- Tailwind over CSS Modules: Team preference and faster development

## Current Project State

Frontend foundation is in place with routing and styling configured. 
Ready to implement core features starting with the dashboard view.

## Next Session Objective

Build the dashboard page with user stats display and quick action buttons.

---

## PROMPT FOR NEXT SESSION

Read and apply this bootstrap template:
https://raw.githubusercontent.com/user/repo/main/templates/dev-base.md

## Project Context
Building a productivity dashboard with Next.js 14 and Tailwind CSS.

## Current Status
Project structure complete. Navigation and styling configured.

## This Session's Goal
Implement dashboard page with:
- User statistics cards
- Recent activity feed
- Quick action buttons

Remember: Say "snapshot" when ready for the next handoff.
```
````

### Customization Points

**Purpose**: Guide users on project-specific adaptation

**Should list**:
- What must be filled in
- What can be modified
- What should stay unchanged

**Format**: Bullet list with explanations

**Example**:
```markdown
## Customization Points

Fill in these sections for your specific project:

### Project Goal
What are you trying to accomplish overall?

### Success Criteria
How will you know when the project is complete?

### Technical Constraints
What limitations or requirements exist? (frameworks, languages, etc.)

### Initial Task
What should the first session focus on?

You can also customize:
- Trigger words (though "snapshot" is recommended for consistency)
- Handoff sections (add domain-specific fields as needed)
- Session numbering scheme (sequential, semantic versions, dates, etc.)
```

### Initial Task

**Purpose**: Placeholder for project-specific work

**Should**:
- Clearly indicate this needs customization
- Provide guidance on what to specify
- Be last section of template

**Format**:
```markdown
## Initial Task

[This section will be customized when you start a new project. 
Specify what the first session should accomplish.]
```

## Platform-Specific Sections

Templates MAY include platform-specific sections:

### Claude-Specific

```markdown
## Claude Project Integration

This template can be added to a Claude Project's custom instructions 
for automatic pattern application. Alternatively, reference it via URL 
in each session.

## Artifact Instructions

When creating substantial content (code, documents, structured data), 
request it as an artifact. Reference artifacts in handoffs by title or ID.
```

### ChatGPT-Specific

```markdown
## Custom Instructions

You can add this template's core instructions to your ChatGPT Custom 
Instructions for persistent pattern application.

## GPT Integration

This template can be packaged as a GPT for easier reuse and sharing.
```

### API-Specific

```markdown
## System Prompt Integration

For API usage, include this template's instructions in the system prompt:

```python
system_prompt = """
{template_instructions}
"""
```
```

## Domain-Specific Extensions

Templates MAY add domain-specific sections:

### Research Template

```markdown
## Research-Specific Handoff Sections

Include these additional sections in research handoffs:

### Sources Consulted
- [Citation 1]
- [Citation 2]

### Key Findings
- [Finding 1]
- [Finding 2]

### Open Questions
- [Question 1]
- [Question 2]
```

### Development Template

```markdown
## Development-Specific Handoff Sections

Include these additional sections in development handoffs:

### Code Changes
- [Module 1]: [Description of changes]
- [Module 2]: [Description of changes]

### Tests Added/Modified
- [Test description]

### Technical Debt
- [Debt item to address later]
```

### Content Template

```markdown
## Content-Specific Handoff Sections

Include these additional sections in content handoffs:

### Content Pieces
- [Piece 1]: [Status and word count]
- [Piece 2]: [Status and word count]

### Editorial Decisions
- [Decision about tone, structure, etc.]

### Review Feedback
- [Feedback item to address]
```

## Template Metadata

Templates SHOULD include metadata at the top:

```markdown
---
template: base-bootstrap
version: 1.0.0
platform: claude
author: username
created: 2025-10-05
updated: 2025-10-05
tags: [workflow, handoff, session-management]
---

# Base Bootstrap Template v1.0
...
```

## Validation

A bootstrap template can be validated against these criteria:

**Required Elements**:
- [ ] Template name and version
- [ ] Workflow pattern explanation
- [ ] Trigger definition
- [ ] Handoff format specification
- [ ] Continuation instructions
- [ ] Initial task section

**Recommended Elements**:
- [ ] Overview/description
- [ ] Example handoff
- [ ] Customization points
- [ ] Important notes

**Quality Checks**:
- [ ] Valid markdown
- [ ] No broken links
- [ ] Clear and unambiguous instructions
- [ ] Example matches format specification
- [ ] Accessible URL (if hosted)
- [ ] Reasonable length (not too verbose)

**Content Quality**:
- [ ] Instructions are specific, not vague
- [ ] Format is well-structured
- [ ] Examples are realistic
- [ ] Customization points are clear
- [ ] No platform-specific assumptions (unless platform-specific template)

## Complete Example Template

```markdown
# Base Bootstrap Template v1.0

## Overview

This template establishes a minimal session handoff workflow for any 
type of LLM project. Use this as a starting point and customize for 
your specific needs.

## Workflow Pattern

This project uses an iterative session handoff pattern:

- Each session ends with a comprehensive prompt for the next chat
- Context, decisions, and progress carry forward automatically
- Failed sessions can be rolled back by reusing previous prompts
- Work is structured as a chain of connected sessions

## Session Handoff Instructions

When the user says **"snapshot"** or **"→"**, generate the next 
session prompt using the format below.

## Handoff Format

```
=== SESSION HANDOFF ===
Generated: [ISO 8601 datetime]
Session: [identifier, e.g., "Session 3 → 4"]

## Previous Session Summary

### Accomplished
- [Key achievement 1]
- [Key achievement 2]
- [Key achievement 3]

### Decisions Made
- [Decision 1]: [Brief rationale]
- [Decision 2]: [Brief rationale]

## Current Project State

[2-4 sentence summary of where the project stands now]

## Next Session Objective

[Clear, specific goal for the next session]

## Context for Next Session

[Any additional context, constraints, or background needed]

---

## PROMPT FOR NEXT SESSION

Copy everything below this line into a new chat:

---

Read and apply this bootstrap template:
https://raw.githubusercontent.com/YOUR-USERNAME/llm-project-templates/main/implementations/claude/bootstrap/base.md

## Project Context

[Include relevant project background]

## Current Status

[Brief summary of progress]

## This Session's Goal

[The specific objective for this session]

---

Remember: Say "snapshot" when ready to generate the next handoff.
```

## Important Notes

- Each generated prompt is self-contained and includes the bootstrap URL
- The pattern perpetuates itself across sessions
- Users can break the chain anytime or customize prompts before using
- This template works with any LLM that can read URLs

## Example Handoff

```
=== SESSION HANDOFF ===
Generated: 2025-10-05T16:45:00Z
Session: Session 1 → 2

## Previous Session Summary

### Accomplished
- Set up project repository structure
- Created initial documentation outline
- Defined project scope and goals

### Decisions Made
- Markdown for documentation: Easy to version control and widely supported
- Weekly session cadence: Allows time for research between sessions

## Current Project State

Project infrastructure is in place. Documentation framework is ready. 
Clear scope defined for the research phase. Ready to begin actual 
research and content creation.

## Next Session Objective

Conduct initial research and create first draft of methodology section.

## Context for Next Session

Focus on qualitative research methods. Review academic sources from 
last 5 years. Aim for 2000-3000 words in methodology section.

---

## PROMPT FOR NEXT SESSION

Copy everything below this line into a new chat:

---

Read and apply this bootstrap template:
https://raw.githubusercontent.com/YOUR-USERNAME/llm-project-templates/main/implementations/claude/bootstrap/base.md

## Project Context

Research project on effective LLM workflow patterns. Goal is to document 
best practices and create reusable templates.

## Current Status

Project setup complete. Repository and documentation structure in place.

## This Session's Goal

Research and draft the methodology section (2000-3000 words) focusing 
on qualitative research methods from recent academic sources.

---

Remember: Say "snapshot" when ready to generate the next handoff.
```

## Customization Points

Fill in these sections for your specific project:

### Project Description
What are you building or researching?

### Project Goal
What is the overall objective?

### Success Criteria
How will you know when you're done?

### Initial Task
What should the first session accomplish?

You can also customize:
- Trigger words (though "snapshot" is recommended)
- Handoff sections (add what you need)
- Session numbering approach

## Initial Task

[This section will be customized when you start a new project. 
Describe what the first session should focus on and accomplish.]
```

## Versioning

Bootstrap templates use semantic versioning:

- **Major (1.x → 2.x)**: Breaking changes to format or pattern
- **Minor (x.1 → x.2)**: New sections or features, backward compatible
- **Patch (x.x.1 → x.x.2)**: Clarifications, typo fixes, examples

Current specification version: 1.0.0

## See Also

- [Handoff Format Specification](./handoff-format.md)
- [Bootstrap Pattern Documentation](../docs/patterns/bootstrap.md)
- [Implementation Guide](../docs/implementation-guide.md)
- [Example Templates](../implementations/)