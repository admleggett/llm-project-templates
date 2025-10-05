# Implementation Guide

This guide helps you adapt the LLM Project Templates patterns for your preferred LLM platform.

## Overview

The core patterns are platform-agnostic, but implementation details vary. This guide walks you through creating an implementation for any LLM.

## Platform Assessment

### Step 1: Identify Platform Capabilities

Answer these questions about your LLM platform:

#### Context Management
- Does it have persistent context features? (Projects, Custom Instructions, GPTs, Gems)
- What's the context window size?
- Can context be explicitly managed across sessions?

#### Structured Output
- Can it create artifacts or structured content?
- Does it support markdown, code blocks, or other formats?
- Can it generate multi-part responses?

#### Tool Integration
- What built-in tools are available? (web search, code execution, etc.)
- Can external tools be integrated?
- How are tool results presented?

#### API Access
- Is there an API for programmatic access?
- Can responses be streamed?
- Is there rate limiting?

### Step 2: Map to Pattern Requirements

The patterns require these capabilities:

| Requirement | Essential? | Platform Feature Needed |
|------------|-----------|------------------------|
| Generate text responses | Yes | Basic LLM capability |
| Read external URLs | Yes | URL fetching or tool use |
| Follow complex instructions | Yes | Instruction following |
| Maintain format consistency | Preferred | Strong instruction adherence |
| Create structured content | Optional | Artifacts or similar |
| Long context | Helpful | 32K+ token window |

## Implementation Steps

### Step 3: Define Trigger Mechanism

Choose how users signal the end of a session:

**Option A: Keywords**
```
Pros: Natural, easy to remember
Examples: "snapshot", "handoff", "checkpoint"
```

**Option B: Symbols**
```
Pros: Concise, unambiguous
Examples: "→", ">>", "///"
```

**Option C: Structured Commands**
```
Pros: Explicit, extensible
Examples: "/handoff", "@snapshot", "#next"
```

**Recommendation**: Start with a simple keyword like "snapshot".

### Step 4: Design Handoff Format

Create a consistent structure for handoff prompts. Essential sections:

```markdown
## Previous Session Summary
[What was accomplished]

## Current Project State
[Where things stand now]

## Next Session Objective
[What to do next]

## Restoration Prompt
[Complete prompt for next session]
```

Optional sections based on your domain:
- Key decisions made
- Artifacts created
- Resources consulted
- Open questions
- Technical constraints

### Step 5: Create Bootstrap Template

Develop a template that:

1. **Explains the pattern** to the LLM
2. **Defines the trigger** for handoff generation
3. **Specifies the format** for handoffs
4. **Includes continuation instructions** so the pattern perpetuates

Minimal bootstrap template structure:

```markdown
# [Platform] Project Bootstrap v1.0

## Workflow Pattern
[Brief explanation of session handoff pattern]

## Instructions
When the user says "[TRIGGER]", generate the next session prompt using this format:

[HANDOFF FORMAT]

Ensure each generated prompt includes:
- A reference to this bootstrap template
- Instructions to continue the pattern

## Initial Task
[Placeholder for project-specific start]
```

### Step 6: Test the Pattern

Create a test project and verify:

- [ ] Bootstrap template is accessible via URL
- [ ] LLM can read and apply the template
- [ ] Handoff generation works consistently
- [ ] Generated prompts maintain format
- [ ] Pattern continues across multiple sessions
- [ ] Rollback works (reusing previous prompts)

### Step 7: Document Platform Specifics

Create a README for your implementation covering:

- Platform-specific features leveraged
- Any limitations or workarounds
- Tips for optimal use
- Example workflows
- Troubleshooting guide

## Platform-Specific Considerations

### ChatGPT

**Key features:**
- Custom Instructions (persistent)
- GPTs (shareable configurations)
- Canvas (artifact-like feature)
- DALL-E integration

**Implementation notes:**
- Use Custom Instructions for pattern instructions
- GPTs can package templates for reuse
- Canvas good for iterative content
- 128K context window

**Template hosting:**
```markdown
Read this bootstrap template:
[URL to template]

Or create a GPT with the template built-in
```

### Claude

**Key features:**
- Projects (custom instructions + knowledge)
- Artifacts (structured content)
- 200K context window
- Extended thinking mode
- Tool use (web search, etc.)

**Implementation notes:**
- Projects ideal for persistent patterns
- Artifacts excellent for evolving content
- Large context allows comprehensive handoffs
- Can reference artifacts in snapshots

**Template hosting:**
```markdown
Read and apply this bootstrap template:
[GitHub raw URL]
```

### Gemini

**Key features:**
- Gems (saved configurations)
- Google Workspace integration
- Long context (1M+ tokens)
- Multimodal capabilities

**Implementation notes:**
- Gems can store bootstrap templates
- Integration with Drive/Docs useful for snapshots
- Massive context enables very long sessions
- Can include images in handoffs

**Template hosting:**
```markdown
Follow this template:
[Google Docs public link or GitHub URL]
```

### API-Based (Generic)

**Key features:**
- Programmatic control
- Any underlying model
- Custom tooling
- Automation potential

**Implementation notes:**
- System prompts for bootstrap
- Can automate snapshot storage
- Programmatic rollback possible
- Version control integrated

**Implementation example:**
```python
system_prompt = load_template("bootstrap/base.md")
conversation = client.chat(
    model="gpt-4",
    system=system_prompt,
    messages=conversation_history
)
```

## Advanced Implementations

### Automated Snapshot Storage

```python
# Automatically save snapshots to git
def on_snapshot_generated(snapshot_content):
    session_num = get_next_session_number()
    filename = f"snapshots/session-{session_num:02d}.md"
    
    with open(filename, 'w') as f:
        f.write(snapshot_content)
    
    subprocess.run(['git', 'add', filename])
    subprocess.run(['git', 'commit', '-m', f'Snapshot: Session {session_num}'])
```

### Interactive Template Selection

```markdown
# Instead of single template:
Read and select appropriate template:

Base patterns:
- https://[...]/base.md - Minimal handoff pattern
- https://[...]/with-artifacts.md - Enhanced with artifacts

Domain templates:
- https://[...]/research.md - Research workflows
- https://[...]/development.md - Software development

Which template best fits: [PROJECT DESCRIPTION]?
```

### Template Composition

```markdown
# Combine multiple templates:
Apply these templates in order:
1. Core workflow: https://[...]/base.md
2. Domain pattern: https://[...]/research.md
3. Team conventions: https://[...]/our-team-standards.md

For project: [DESCRIPTION]
```

### Conditional Handoffs

```markdown
# Different handoff formats based on context:
If session completed successfully: use standard handoff format
If session encountered issues: include troubleshooting section
If major decision made: include decision record format
If artifact created: reference artifact explicitly
```

## Quality Guidelines

### Effective Bootstrap Templates

**Do:**
- Be specific about format requirements
- Include concrete examples
- Explain the "why" behind patterns
- Provide customization points
- Test on real projects first

**Don't:**
- Make assumptions about user context
- Use platform-specific jargon unnecessarily
- Over-constrain the workflow
- Neglect error cases
- Forget continuation instructions

### Effective Handoff Prompts

**Do:**
- Summarize concisely but completely
- Highlight key decisions with rationale
- Make next objectives clear and actionable
- Include all necessary context
- Reference the bootstrap template

**Don't:**
- Reproduce entire conversations
- Include exploratory dead-ends
- Be vague about next steps
- Lose track of the overall goal
- Forget to include pattern instructions

## Troubleshooting

### Template Not Applied

**Problem:** LLM doesn't follow template instructions

**Solutions:**
- Verify template URL is accessible
- Check template formatting (markdown syntax)
- Make instructions more explicit
- Add examples to template
- Test with simpler template first

### Handoffs Lose Quality

**Problem:** Generated handoffs degrade over sessions

**Solutions:**
- Strengthen format specification in template
- Add examples of good handoffs to template
- Reduce handoff length requirements
- Reset from earlier snapshot
- Revise template based on failure patterns

### Pattern Doesn't Continue

**Problem:** Later sessions don't maintain pattern

**Solutions:**
- Ensure bootstrap URL in generated prompts
- Make continuation instructions more explicit
- Add "remember to include this template" reminder
- Check that handoff format is preserved
- Verify platform consistently reads URLs

### Context Overflow

**Problem:** Handoffs become too long

**Solutions:**
- Summarize more aggressively
- Reference artifacts rather than including content
- Use differential snapshots (only changes)
- Split into multiple projects
- Increase summary compression in template

## Contributing Your Implementation

Once you've created an implementation for a new platform:

1. **Create directory structure:**
   ```
   implementations/[platform-name]/
   ├── README.md
   ├── bootstrap/
   │   └── base.md
   └── examples/
       └── sample-handoff.md
   ```

2. **Document thoroughly:**
   - Platform capabilities
   - Setup instructions
   - Usage examples
   - Known limitations
   - Tips and tricks

3. **Test comprehensively:**
   - Multiple session workflow
   - Rollback scenario
   - Different project types
   - Edge cases

4. **Submit pull request:**
   - Reference this implementation guide
   - Explain platform-specific choices
   - Include working examples
   - Update root README

## Next Steps

- Review existing [Claude implementation](../implementations/claude/)
- Explore [pattern documentation](./patterns/)
- Check [examples](../examples/) for inspiration
- Join community discussions
- Share your implementation!

## Resources

- [Session Handoff Pattern](./patterns/session-handoff.md)
- [Snapshot Pattern](./patterns/snapshots.md)
- [Bootstrap Pattern](./patterns/bootstrap.md)
- [Contributing Guide](./contributing.md)