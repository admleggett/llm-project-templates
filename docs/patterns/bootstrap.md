# Bootstrap Pattern

## Intent

Provide reusable templates that initialize LLM sessions with predefined workflow patterns, instructions, and structures, enabling consistent and efficient project setup.

## Also Known As

- Template Method
- Project scaffolding
- Initialization pattern

## Motivation

Starting new LLM projects often involves:

- Repeating the same setup instructions
- Explaining workflow patterns each time
- Inconsistent session structures
- Lost time on boilerplate setup

Bootstrap templates solve this by packaging common patterns into reusable, version-controlled resources that can be quickly applied to new projects.

## Applicability

Use bootstrap templates when:

- Multiple projects share common workflow patterns
- Setup instructions are complex or lengthy
- Consistency across projects is valuable
- You want to share proven patterns with others
- Iteration on the pattern itself is needed

## Structure

```
┌─────────────────────┐
│  Abstract Template  │
│                     │
│  + initialize()     │
│  + defineWorkflow() │
│  + setupHandoffs()  │
└─────────────────────┘
          △
          │
          │ inherits/specializes
          │
    ┌─────┴─────┬─────────────┬──────────────┐
    │           │             │              │
┌───▼────┐  ┌──▼──────┐  ┌───▼────────┐  ┌─▼────────────┐
│  Base  │  │Research │  │Development │  │   Content    │
│Template│  │Template │  │  Template  │  │   Template   │
└────────┘  └─────────┘  └────────────┘  └──────────────┘
```

## Participants

### Abstract Template
- Defines workflow skeleton
- Specifies handoff format
- Includes pattern instructions
- Provides customisation points

### Concrete Template
- Specializes abstract template for domain
- Adds domain-specific structure
- Includes relevant examples
- Defines domain triggers/conventions

### Session
- Initialized from template
- Follows template workflow
- Generates handoffs per template format

## Collaborations

1. User selects appropriate template
2. User customises template for specific project
3. User provides template URL to LLM session
4. LLM reads template and applies instructions
5. Session follows template workflow
6. Generated handoffs include template reference
7. Subsequent sessions maintain pattern consistency

## Consequences

### Benefits

**Rapid setup**: Projects start quickly with proven patterns already in place.

**Consistency**: All projects using the same template follow the same workflow.

**Shareability**: Templates can be shared across teams or open-sourced.

**Iteration**: Templates can be improved; all future projects benefit.

**Documentation**: Templates serve as documentation of best practices.

**Onboarding**: New team members can follow established patterns easily.

### Liabilities

**Rigidity**: Templates might not fit all use cases perfectly.

**Versioning complexity**: Updating templates doesn't affect existing projects.

**Learning curve**: Understanding template structure takes initial effort.

**Maintenance**: Templates need to be kept up-to-date.

## Implementation

### Template Structure

```markdown
# [Template Name] v[Version]

## Pattern Description
[What this template does]

## Workflow Instructions
[Step-by-step pattern to follow]

## Handoff Format
[Specific format for this template]

## Triggers
[Keywords/commands for actions]

## Customization Points
[What should be filled in per-project]

## Example Usage
[Sample of template in action]

---

## Initial Task
[Placeholder for project-specific starting point]
```

### Hosting Strategy

**GitHub (recommended)**:
```
https://raw.githubusercontent.com/user/repo/main/templates/base.md
```

**Benefits**:
- Version control
- Public accessibility
- Easy updates
- Fork-able by others

**Alternative hosting**:
- Google Docs (public)
- Gists
- Personal website
- Corporate wiki

### Usage Pattern

```markdown
# User starts new session:

Read and apply this bootstrap template:
[template URL]

Project: [specific project description]
Initial task: [what to start with]

# LLM fetches and applies template automatically
```

### Template Composition

Templates can be layered:

```markdown
Read and apply these templates:
1. Base workflow: [base-template-url]
2. Domain-specific: [research-template-url]

Then initialize for: [specific project]
```

## Sample Code

### Base Bootstrap Template

```markdown
# Base Bootstrap Template v1.0

## Workflow Pattern

This template establishes a session handoff workflow:
- Each session ends with a comprehensive next-session prompt
- Context carries forward automatically
- Rollback is possible via previous snapshots

## Session Handoff Instructions

When user says "snapshot" or "→", generate the next prompt using:

```
=== SESSION HANDOFF ===
[standard format here]
```

## Customization Points

Fill in these sections for your specific project:

### Project Goal
[What are you trying to accomplish?]

### Success Criteria
[How will you know when you're done?]

### Constraints
[What limitations or requirements exist?]

## Initial Task

[Specify what to start working on]
```

### Domain-Specific Template

```markdown
# Research Project Template v1.0

Extends: Base Bootstrap Template

## Additional Instructions

For research workflows:

1. Track sources with citations
2. Maintain a "findings" section
3. Note open questions
4. Generate literature review summaries

## Enhanced Handoff Format

In addition to base handoff, include:

### Sources Consulted
- [Source 1: key findings]
- [Source 2: key findings]

### Open Questions
- [Question 1]
- [Question 2]

### Research Direction
[How inquiry should proceed]

## Research-Specific Triggers

- "literature review": Generate summary of sources
- "open questions": List current unknowns
- "synthesis": Create integrated findings document

## Initial Research Question

[Specify the research question to investigate]
```

### Project-Specific Instance

```markdown
# User's actual project initialization:

Read and apply this bootstrap template:
https://[...]/research-template.md

## Project Details

Research question: 
"What are the most effective interventions for reducing 
carbon emissions in urban transportation?"

Success criteria:
- Identify top 5 intervention types
- Quantify effectiveness of each
- Provide implementation examples
- Assess feasibility and costs

Constraints:
- Focus on cities with >1M population
- Published research from last 10 years
- Peer-reviewed sources preferred

Initial task:
Conduct literature search and create taxonomy of intervention types
```

## Variants

### Minimal Template
Just the essential pattern, maximum flexibility:
```markdown
When user says "snapshot", generate next prompt.
Include this template URL in all prompts.
```

### Comprehensive Template
Detailed instructions, examples, multiple triggers:
```markdown
[Extensive workflow definition]
[Multiple handoff formats]
[Domain-specific conventions]
[Examples and anti-patterns]
```

### Composable Templates
Designed to be combined:
```markdown
# Base Layer
[Core workflow]

# Feature Layer
[Additional capabilities]

# Domain Layer
[Specific use case]
```

### Interactive Template
Asks questions during initialization:
```markdown
Before starting, please answer:
1. What is your primary goal?
2. What's your timeline?
3. What constraints exist?

[Template adapts based on answers]
```

## Known Uses

### Software Development
- Sprint planning templates
- Code review workflows
- Architecture decision workflows
- Bug investigation patterns

### Research
- Literature review templates
- Experiment design workflows
- Data analysis patterns
- Paper writing structures

### Content Creation
- Article writing workflows
- Documentation patterns
- Tutorial development
- Marketing copy frameworks

### Business Analysis
- Market research templates
- Competitive analysis workflows
- Strategy development patterns
- Decision-making frameworks

## Template Gallery Example

```
templates/
├── base/
│   ├── minimal.md          # Bare bones pattern
│   └── full-featured.md    # All bells and whistles
├── development/
│   ├── web-app.md         # Web development projects
│   ├── cli-tool.md        # Command line tools
│   └── library.md         # Library development
├── research/
│   ├── literature-review.md
│   ├── data-analysis.md
│   └── hypothesis-testing.md
└── content/
    ├── blog-post.md
    ├── documentation.md
    └── tutorial.md
```

## Best Practices

### Template Design

**Be specific about format**: Don't say "summarize previous work", say:
```markdown
### Previous Work
- [Achievement 1]
- [Achievement 2]
[Maximum 5 items]
```

**Include examples**: Show what good output looks like.

**Provide escape hatches**: Allow users to deviate when needed.

**Version your templates**: Use semantic versioning for clarity.

**Document assumptions**: State what the template assumes about the workflow.

### Template Maintenance

**Collect feedback**: Track what works and what doesn't.

**Iterate regularly**: Update based on real usage.

**Maintain changelog**: Help users understand what changed.

**Test templates**: Try them on real projects before publishing.

**Deprecate gracefully**: Give notice before removing old versions.

### Template Usage

**Start simple**: Use minimal templates first, add complexity as needed.

**Customise freely**: Templates are starting points, not constraints.

**Share improvements**: Contribute enhancements back to community.

**Document deviations**: Note when/why you diverge from template.

## Related Patterns

### Template Method (GoF)
Bootstrap templates are essentially the Template Method pattern applied to LLM workflows.

### Strategy
Different templates can be viewed as different strategies for structuring LLM work.

### Factory
Bootstrap templates act as factories for creating configured LLM sessions.

### Session Handoff
Bootstrap templates define how handoffs should work.

## See Also

- [Template Method Pattern (GoF)](https://en.wikipedia.org/wiki/Template_method_pattern)
- [Session Handoff Pattern](./session-handoff.md)
- [Snapshot Pattern](./snapshots.md)