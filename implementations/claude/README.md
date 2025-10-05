# Claude Implementation

This directory contains templates and examples for using the LLM Project Templates pattern with Claude (Anthropic).

## Features

Claude-specific features leveraged in this implementation:

- **Projects**: Custom instructions and knowledge base
- **Artifacts**: For creating and updating structured content
- **Long context**: 200K token context window
- **Tool use**: Integration with web search and other capabilities

## Bootstrap Templates

### base.md
Minimal implementation of the session handoff pattern. Best for:
- Learning the pattern
- Simple workflows
- Projects that don't need artifacts

### with-artifacts.md
Enhanced version that leverages Claude's artifact system. Best for:
- Projects producing documents, code, or structured content
- Maintaining evolving artifacts across sessions
- Visual or interactive content

## Quick Start

1. **Copy the raw URL** of your chosen bootstrap template:
   ```
   https://raw.githubusercontent.com/YOUR-USERNAME/llm-project-templates/main/implementations/claude/bootstrap/base.md
   ```

2. **Start a new Claude chat** and paste:
   ```
   Read and apply this bootstrap template:
   [paste URL]
   
   Project: [describe what you're building]
   Initial task: [what to start with]
   ```

3. **Work through the session** naturally

4. **When ready to end**, say: `snapshot`

5. **Copy the generated prompt** and use it to start your next session

6. **If a session fails**, delete it and use the previous snapshot

## Project Templates

The `project-templates/` directory contains domain-specific templates:

- `research/` - Literature review, data analysis, investigation workflows
- `development/` - Software projects, coding tasks, technical writing
- `content-creation/` - Articles, documentation, creative writing

Each combines the handoff pattern with domain-specific structure.

## Examples

See the `examples/` directory for:
- Complete session handoff examples
- Successful multi-session workflows
- Rollback scenarios
- Common patterns and variations

## Tips for Claude

### Leveraging Projects
Consider adding the bootstrap template to your Claude Project's custom instructions for automatic pattern application.

### Using Artifacts
Request artifacts for any substantial content you'll want to reference or iterate on across sessions.

### Triggering Snapshots
You can customize the trigger word - just specify it in your initial prompt:
```
Use "checkpoint" instead of "snapshot" to generate handoffs
```

### Modifying Generated Prompts
The generated prompts are starting points - feel free to edit before using:
- Add new constraints
- Change the objective
- Include additional context
- Adjust the scope

## Claude-Specific Patterns

### Artifact Continuity
When working with artifacts across sessions:
1. Note artifact IDs in snapshots
2. Reference them in next session prompt
3. Request updates rather than recreating

### Search Integration
For research workflows, include search results in handoffs:
```
At snapshot, include: key findings from searches, relevant URLs, 
important quotes (properly cited)
```

### Long Context Advantage
Claude's 200K context means you can:
- Have longer individual sessions
- Include more comprehensive handoff prompts
- Reference extensive prior work

## Troubleshooting

### Handoff prompt too long
- Summarize accomplishments more concisely
- Reference artifacts rather than including full content
- Focus on decisions and next steps, not full history

### Pattern not continuing
- Ensure bootstrap URL is in generated prompts
- Check that handoff instructions are clear
- Verify the template URL is accessible

### Lost context
- Store successful snapshots in git
- Keep a session log with timestamps
- Use descriptive session numbers

## Next Steps

- Explore [project templates](./project-templates/) for domain-specific workflows
- Review [examples](./examples/) to see the pattern in action
- Customize bootstrap templates for your specific needs