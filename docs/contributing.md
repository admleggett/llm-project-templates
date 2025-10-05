# Contributing Guide

Thank you for your interest in contributing to LLM Project Templates! This guide will help you contribute effectively.

## Ways to Contribute

### 1. New Platform Implementations

Adapt the patterns for additional LLM platforms:
- ChatGPT
- Gemini
- Open-source models (Llama, Mistral, etc.)
- Platform-specific tools (Cursor, Continue, etc.)

See [Implementation Guide](./implementation-guide.md) for details.

### 2. Domain-Specific Templates

Create templates for specific use cases:
- Research methodologies
- Software development workflows
- Content creation patterns
- Business analysis frameworks
- Educational applications

### 3. Pattern Documentation

Improve or expand pattern documentation:
- Clarify existing patterns
- Add new patterns
- Provide more examples
- Create visual diagrams
- Write tutorials

### 4. Examples

Contribute real-world workflow examples:
- Complete session sequences
- Successful project handoffs
- Rollback scenarios
- Edge cases and solutions

### 5. Bug Fixes & Improvements

- Fix documentation errors
- Improve template clarity
- Enhance markdown formatting
- Update broken links
- Refine examples

## Contribution Process

### 1. Check Existing Issues

Before starting work:
- Review open issues
- Check pull requests
- Search discussions
- Avoid duplicate work

### 2. Open an Issue First

For significant contributions:
- Describe what you want to add
- Explain the motivation
- Discuss approach
- Get feedback before coding

For minor fixes:
- Pull requests welcome directly

### 3. Fork and Branch

```bash
# Fork the repository on GitHub
# Clone your fork
git clone https://github.com/admleggett/llm-project-templates.git
cd llm-project-templates

# Create a branch
git checkout -b feature/your-feature-name
# or
git checkout -b fix/issue-description
```

### 4. Make Your Changes

Follow the contribution guidelines below.

### 5. Test Your Changes

- Verify markdown renders correctly
- Test any templates you create
- Check links work
- Ensure examples are accurate
- Proofread documentation

### 6. Commit

Use clear, descriptive commit messages:

```bash
# Good commit messages:
git commit -m "Add ChatGPT bootstrap template"
git commit -m "Fix broken link in implementation guide"
git commit -m "Improve session handoff pattern documentation"

# Less helpful:
git commit -m "Update files"
git commit -m "Fix stuff"
```

### 7. Push and Create Pull Request

```bash
git push origin feature/your-feature-name
```

Then create a pull request on GitHub with:
- Clear title
- Description of changes
- Reference to related issues
- Screenshots if relevant

## Contribution Guidelines

### New Platform Implementations

When adding a new platform implementation:

**Required files:**
```
implementations/[platform-name]/
├── README.md              # Platform overview and usage
├── bootstrap/
│   └── base.md           # At minimum, one bootstrap template
└── examples/
    └── sample-handoff.md # At least one example
```

**README.md should include:**
- Platform name and capabilities
- Installation/setup instructions
- Quick start guide
- Platform-specific features
- Limitations and workarounds
- Links to platform documentation

**Bootstrap template should include:**
- Clear pattern explanation
- Trigger mechanism
- Handoff format specification
- Continuation instructions
- Customization points

**Examples should show:**
- Complete handoff cycle
- Actual generated prompts
- Real project usage

### Domain Templates

When creating domain-specific templates:

**Structure:**
```
implementations/[platform]/project-templates/[domain]/
├── README.md
└── template.md
```

**Template should include:**
- Domain-specific workflow
- Relevant triggers/commands
- Specialized handoff sections
- Domain conventions
- Example usage

**Domains to consider:**
- research (literature review, experiments, analysis)
- development (coding, debugging, architecture)
- content (writing, documentation, marketing)
- business (strategy, analysis, planning)
- education (curriculum, lessons, assessments)

### Documentation

When improving documentation:

**Follow markdown conventions:**
- Use headers hierarchically (h1 → h2 → h3)
- Include code fences with language tags
- Add blank lines between sections
- Use relative links for internal references
- Include a table of contents for long docs

**Writing style:**
- Clear and concise
- Active voice preferred
- Define technical terms
- Include examples
- Avoid jargon when possible

**Pattern documentation structure:**
- Intent
- Motivation
- Applicability
- Structure
- Participants
- Consequences
- Implementation
- Examples
- Related patterns

### Examples

When adding examples:

**Include context:**
- What type of project
- What was the goal
- What platform was used
- What template was applied

**Show progression:**
- Initial prompt
- Session work (summarized)
- Generated handoff
- Next session initialization
- Results

**Annotate when helpful:**
```markdown
# Session 2 Handoff

=== SESSION HANDOFF ===
Session 2 → 3

## Previous Session Summary
- Completed data model design  ← Key accomplishment
- Decided on PostgreSQL        ← Important decision
...
```

### Code Examples

When including code:

**Use proper formatting:**
```markdown
```python
# Python code here
```

```bash
# Shell commands here
```
```

**Ensure code is:**
- Tested and working
- Well-commented
- Following best practices
- Appropriate for the example

## Review Process

### What Reviewers Look For

**Content quality:**
- Accuracy of information
- Clarity of explanation
- Completeness of examples
- Proper formatting

**Usability:**
- Easy to understand
- Practical and actionable
- Well-organized
- Properly linked

**Consistency:**
- Matches existing style
- Follows conventions
- Integrates well with existing content

### Addressing Feedback

- Be open to suggestions
- Ask questions if unclear
- Make requested changes
- Update PR description as needed
- Re-request review when ready

## Style Guide

### Markdown

**Headers:**
```markdown
# H1 for page title only
## H2 for major sections
### H3 for subsections
#### H4 sparingly
```

**Lists:**
```markdown
- Unordered lists for non-sequential items
1. Ordered lists for sequential steps
```

**Emphasis:**
```markdown
*Italic* for emphasis
**Bold** for strong emphasis
`code` for inline code/commands
```

**Links:**
```markdown
[Descriptive text](./relative/path.md)
[External link](https://example.com)
```

**Code blocks:**
````markdown
```language
code here
```
````

### Naming Conventions

**Files:**
- Lowercase with hyphens: `session-handoff.md`
- Descriptive names: `claude-bootstrap-base.md`

**Directories:**
- Lowercase, no spaces: `implementations/`
- Descriptive: `project-templates/`

**Branches:**
- `feature/description` for new features
- `fix/description` for bug fixes
- `docs/description` for documentation

### Template Versioning

Templates should include version numbers:
```markdown
# Template Name v1.0
# Template Name v1.1
# Template Name v2.0
```

Version updates:
- **Major (v1 → v2)**: Breaking changes to format or pattern
- **Minor (v1.0 → v1.1)**: New features, backward compatible
- **Patch (v1.1 → v1.1.1)**: Bug fixes, clarifications

## Community Guidelines

### Be Respectful

- Assume good intentions
- Provide constructive feedback
- Welcome newcomers
- Value diverse perspectives

### Be Helpful

- Answer questions patiently
- Share knowledge freely
- Provide context and examples
- Link to relevant documentation

### Be Collaborative

- Discuss before diverging
- Build on others' work
- Give credit appropriately
- Work together on solutions

## Recognition

Contributors will be:
- Listed in project documentation
- Credited in release notes
- Acknowledged in relevant sections
- Appreciated! 🎉

## Questions?

- Open an issue for general questions
- Start a discussion for ideas
- Check existing documentation
- Reach out to maintainers

## License

By contributing, you agree that your contributions will be licensed under the same [MIT License](../LICENSE) as the project.

Thank you for contributing to LLM Project Templates!