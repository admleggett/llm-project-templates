# LLM Project Templates

Version-controlled templates and patterns for managing complex work across multiple LLM chat sessions.

## The Problem

Working on substantial projects with LLMs often involves:
- Long conversations that hit context limits
- Lost context when starting fresh sessions
- Difficulty tracking decisions and progress
- No rollback when a session goes off-track

## The Solution

This repository provides templates that enable:
- **Session handoffs**: Each chat generates a prompt for the next
- **Context preservation**: Decisions and progress carry forward
- **Version control**: Snapshot successful states
- **Rollback capability**: Revert to previous checkpoints
- **Bootstrap patterns**: Quick-start new projects with proven workflows

## Current Implementation

- ✅ **Claude** - Full implementation with Projects and Artifacts support
- 🔜 ChatGPT, Gemini, API-based workflows

## Quick Start (Claude)

1. Choose a bootstrap template:
   ```
   https://raw.githubusercontent.com/admleggett/llm-project-templates/main/implementations/claude/bootstrap/base.md
   ```

2. Start a new Claude chat:
   ```
   Read and apply this bootstrap template:
   [paste URL above]
   
   Project: [describe your project]
   Initial task: [what to start with]
   ```

3. At session end, say **"snapshot"** to generate the next prompt

4. Start new session with that generated prompt

5. If a session fails, delete it and use the previous snapshot

See [full documentation](./docs/overview.md) for details.

## Patterns Used

This framework implements several software design patterns:

- **Chain of Responsibility**: Sessions pass context forward as handlers
- **Memento**: Snapshots capture state for rollback
- **Template Method**: Bootstrap templates define workflow structure

See [Pattern Documentation](./docs/patterns/) for detailed explanations.

## Repository Structure

```
llm-project-templates/
├── implementations/     # Platform-specific implementations
│   └── claude/         # Claude (Anthropic) implementation
├── docs/               # Documentation and guides
├── spec/               # Abstract specifications
└── examples/           # Real-world workflow examples
```

## Contributing

We welcome implementations for other LLM platforms! See our [Contributing Guide](./docs/contributing.md).

## License

MIT License - See [LICENSE](./LICENSE) for details.