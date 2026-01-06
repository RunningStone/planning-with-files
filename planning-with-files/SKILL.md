---
name: planning-with-files
description: Transforms workflow to use Manus-style persistent markdown files for planning, progress tracking, and knowledge storage. Use when starting complex tasks, multi-step projects, research tasks, or when the user mentions planning, organizing work, tracking progress, or wants structured output.
---

# Planning with Files

Work like Manus: Use persistent markdown files as your "working memory on disk."

## Quick Start

Before ANY complex task:

1. **Create `CLAUDE_DOCs/task_plan.md`** in the project root
2. **Define phases** with checkboxes
3. **Update after each phase** - mark [x] and change status
4. **Archive plan changes** to `PLAN_TIMELINE/` when modifying the plan structure
5. **Read before deciding** - refresh goals in attention window

## Directory Structure

All Claude-generated documents go in `CLAUDE_DOCs/` under project root:

```
project_root/
└── CLAUDE_DOCs/
    ├── task_plan.md              # Current active plan
    ├── notes.md                  # Research notes
    ├── [deliverable].md          # Final deliverables
    │
    ├── PLAN_TIMELINE/            # Plan version history
    │   ├── OVERALL.md            # Changelog: timestamp | change purpose
    │   └── YYYYMMDD_HHMMSS.md    # Historical snapshots
    │
    ├── Design/                   # Design documents
    │   ├── OVERALL.md            # Index: filename | design purpose
    │   └── YYYYMMDD_vN_type.md   # e.g., 20260106_v1_算法设计.md
    │
    └── ResultsAnalysis/          # Results and analysis
        ├── OVERALL.md            # Index: filename | key conclusion
        └── YYYYMMDD_vN_type.md   # e.g., 20260106_v1_结果报告.md
```

## The Core File Pattern

For every non-trivial task, create these files in `CLAUDE_DOCs/`:

| File | Purpose | When to Update |
|------|---------|----------------|
| `CLAUDE_DOCs/task_plan.md` | Track phases and progress | After each phase |
| `CLAUDE_DOCs/notes.md` | Store findings and research | During research |
| `CLAUDE_DOCs/[deliverable].md` | Final output | At completion |

## Core Workflow

```
Loop 1: Create CLAUDE_DOCs/task_plan.md with goal and phases
Loop 2: Research → save to CLAUDE_DOCs/notes.md → update task_plan.md
Loop 3: Read CLAUDE_DOCs/notes.md → create deliverable in CLAUDE_DOCs/ → update CLAUDE_DOCs/task_plan.md
Loop 4: Deliver final output
```

### The Loop in Detail

**Before each major action:**
```bash
Read CLAUDE_DOCs/task_plan.md  # Refresh goals in attention window
```

**After each phase:**
```bash
Edit CLAUDE_DOCs/task_plan.md  # Mark [x], update status
```

**When storing information:**
```bash
Write CLAUDE_DOCs/notes.md     # Don't stuff context, store in file
```

**When modifying plan structure (see Plan Change Rules):**
```bash
Copy task_plan.md → PLAN_TIMELINE/YYYYMMDD_HHMMSS.md
Append to PLAN_TIMELINE/OVERALL.md
Then edit task_plan.md
```

## task_plan.md Template

Create `CLAUDE_DOCs/task_plan.md` FIRST for any complex task:

```markdown
# Task Plan: [Brief Description]

## Goal
[One sentence describing the end state]

## Phases
- [ ] Phase 1: Plan and setup
- [ ] Phase 2: Research/gather information
- [ ] Phase 3: Execute/build
- [ ] Phase 4: Review and deliver

## Key Questions
1. [Question to answer]
2. [Question to answer]

## Decisions Made
- [Decision]: [Rationale]

## Errors Encountered
- [Error]: [Resolution]

## Status
**Currently in Phase X** - [What I'm doing now]
```

## notes.md Template

For research and findings (`CLAUDE_DOCs/notes.md`):

```markdown
# Notes: [Topic]

## Sources

### Source 1: [Name]
- URL: [link]
- Key points:
  - [Finding]
  - [Finding]

## Synthesized Findings

### [Category]
- [Finding]
- [Finding]
```

## PLAN_TIMELINE: Version Control for Plans

### What Counts as a "Plan Change" (requires archiving)
- ✅ Add/remove/reorder Phases
- ✅ Modify Goal statement
- ✅ Change Key Questions
- ✅ Significant restructuring

### What Does NOT Count (no archiving needed)
- ❌ Checking off a checkbox `[ ]` → `[x]`
- ❌ Updating Status section
- ❌ Adding to Errors Encountered
- ❌ Adding to Decisions Made

### PLAN_TIMELINE/OVERALL.md Format
```markdown
# Plan Timeline

| Timestamp | Change Purpose |
|-----------|----------------|
| 20260106_113000 | Initial plan created |
| 20260106_150000 | Added Phase 5 for deployment |
| 20260107_091500 | Restructured phases after discovering new requirements |
```

### Workflow for Plan Changes
1. Copy current `task_plan.md` to `PLAN_TIMELINE/YYYYMMDD_HHMMSS.md`
2. Append new row to `PLAN_TIMELINE/OVERALL.md`
3. Edit `task_plan.md` with the changes

## Design/ Folder

Store design documents for algorithms, architecture, experiments, tests.

### File Naming Convention
```
YYYYMMDD_vN_设计类型.md
```

**Design Types:**
- `算法设计` - Algorithm design
- `架构设计` - Architecture design
- `实验设计` - Experiment design
- `测试设计` - Test design

### Design/OVERALL.md Format
```markdown
# Design Documents

| Filename | Purpose |
|----------|----------|
| 20260106_v1_算法设计.md | Core sorting algorithm for data pipeline |
| 20260106_v1_架构设计.md | Microservice architecture for user module |
| 20260107_v2_算法设计.md | Optimized algorithm with caching |
```

## ResultsAnalysis/ Folder

Store experiment results, performance reports, and analysis.

### File Naming Convention
```
YYYYMMDD_vN_报告类型.md
```

**Report Types:**
- `结果报告` - Results report
- `结果分析` - Results analysis
- `性能报告` - Performance report
- `实验报告` - Experiment report

### ResultsAnalysis/OVERALL.md Format
```markdown
# Results Analysis

| Filename | Key Conclusion |
|----------|----------------|
| 20260106_v1_结果报告.md | Baseline accuracy: 85.2% |
| 20260107_v1_结果分析.md | Caching improved throughput by 3x |
```

## Critical Rules

### 1. ALWAYS Create Plan First
Never start a complex task without `CLAUDE_DOCs/task_plan.md`. This is non-negotiable.

### 2. Read Before Decide
Before any major decision, read the plan file. This keeps goals in your attention window.

### 3. Update After Act
After completing any phase, immediately update the plan file:
- Mark completed phases with [x]
- Update the Status section
- Log any errors encountered

### 4. Archive Before Restructure
Before modifying plan structure (phases, goals, questions), archive to `PLAN_TIMELINE/`.

### 5. Store, Don't Stuff
Large outputs go to files, not context. Keep only paths in working memory.

### 6. Log All Errors
Every error goes in the "Errors Encountered" section. This builds knowledge for future tasks.

### 7. Index All Documents
Every file in `Design/` or `ResultsAnalysis/` must have an entry in its `OVERALL.md`.

## When to Use This Pattern

**Use CLAUDE_DOCs pattern for:**
- Multi-step tasks (3+ steps)
- Research tasks
- Building/creating something
- Tasks spanning multiple tool calls
- Anything requiring organization

**Use Design/ folder for:**
- Algorithm design documents
- Architecture decisions
- Experiment design
- Test plans

**Use ResultsAnalysis/ folder for:**
- Experiment results
- Performance benchmarks
- Analysis reports

**Skip for:**
- Simple questions
- Single-file edits
- Quick lookups

## Anti-Patterns to Avoid

| Don't | Do Instead |
|-------|------------|
| Put docs in project root | Use `CLAUDE_DOCs/` folder |
| Overwrite plan without history | Archive to `PLAN_TIMELINE/` first |
| State goals once and forget | Re-read plan before each decision |
| Hide errors and retry | Log errors to plan file |
| Stuff everything in context | Store large content in files |
| Start executing immediately | Create plan file FIRST |
| Create design docs without index | Always update `OVERALL.md` |

## Advanced Patterns

See [reference.md](reference.md) for:
- Attention manipulation techniques
- Error recovery patterns
- Context optimization from Manus

See [examples.md](examples.md) for:
- Real task examples
- Complex workflow patterns
