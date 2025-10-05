# Research Project Example

This example demonstrates using the session handoff pattern for a multi-session research project.

## Project Overview

**Goal**: Investigate the effectiveness of carbon reduction interventions in urban transportation

**Platform**: Claude

**Template Used**: [Base Bootstrap Template](../../implementations/claude/bootstrap/base.md)

**Sessions**: 3 sessions over 2 days

## Session Flow

### Session 1: Initial Research & Taxonomy

**Objective**: Conduct literature search and create taxonomy of intervention types

**Accomplishments**:
- Searched academic databases for relevant papers
- Identified 6 major intervention categories
- Created initial taxonomy structure
- Noted 15 key sources for detailed review

**Key Decision**: Focus on peer-reviewed studies from 2020-2025 for most current data

**Generated Handoff**: [session-01-handoff.md](./session-01-handoff.md)

### Session 2: Deep Dive Analysis

**Objective**: Analyse effectiveness data for each intervention category

**Accomplishments**:
- Analysed 15 key sources in detail
- Quantified effectiveness metrics for each category
- Identified top 5 intervention types
- Noted implementation challenges

**Key Decision**: Use CO2 reduction percentage as primary effectiveness metric

**Generated Handoff**: [session-02-handoff.md](./session-02-handoff.md)

### Session 3: Synthesis & Recommendations

**Objective**: Create final synthesis with recommendations

**Accomplishments**:
- Synthesized findings into coherent report
- Ranked interventions by effectiveness and feasibility
- Provided implementation examples
- Created executive summary

**Output**: Final research report (not included in this example)

## Key Learnings

### What Worked Well

**Clear objectives**: Each session had a specific, achievable goal that kept work focused.

**Citation tracking**: Including sources in handoffs maintained research rigor across sessions.

**Iterative refinement**: Each session built cleanly on previous work without redundancy.

### Challenges

**Source overload**: Initial session identified too many sources; had to narrow scope in session 2.

**Metric consistency**: Some sources used different effectiveness metrics, requiring normalization.

## Handoff Pattern Usage

### Triggers Used
- "snapshot" at end of sessions 1 and 2
- Modified generated prompt slightly for session 3 to add time constraint

### Format Customization

Added research-specific sections to handoffs:
```markdown
### Sources Consulted
[Full citations]

### Key Findings
[Major insights]

### Open Questions
[What still needs investigation]
```

### Rollback Example

During session 2, an initial approach proved unfruitful. Deleted that chat and restarted from session 1 handoff with modified objective focusing on different analysis method.

## Files in This Example

- `README.md` - This file
- `session-01-handoff.md` - Handoff from first to second session
- `session-02-handoff.md` - Handoff from second to third session

## Replicating This Pattern

To use this pattern for your own research:

1. Start with the [base template](../../implementations/claude/bootstrap/base.md)
2. Add research-specific sections (sources, findings, questions)
3. Use clear, specific objectives for each session
4. Track citations consistently
5. Generate handoffs when you reach a natural breakpoint

## Time Investment

- Session 1: ~45 minutes
- Session 2: ~60 minutes  
- Session 3: ~40 minutes
- Total: ~2.5 hours of active work across 2 days

The pattern overhead (generating/using handoffs) added approximately 5 minutes per session but saved significant time by maintaining context and avoiding redundant explanation.