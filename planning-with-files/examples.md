# Examples: Planning with Files in Action

## Example 1: Research Task

**User Request:** "Research the benefits of morning exercise and write a summary"

### Loop 1: Create Plan
```bash
Write CLAUDE_DOCs/task_plan.md
Write CLAUDE_DOCs/PLAN_TIMELINE/OVERALL.md  # Initialize timeline
```

```markdown
# Task Plan: Morning Exercise Benefits Research

## Goal
Create a research summary on the benefits of morning exercise.

## Phases
- [ ] Phase 1: Create this plan ✓
- [ ] Phase 2: Search and gather sources
- [ ] Phase 3: Synthesize findings
- [ ] Phase 4: Deliver summary

## Key Questions
1. What are the physical health benefits?
2. What are the mental health benefits?
3. What scientific studies support this?

## Status
**Currently in Phase 1** - Creating plan
```

### Loop 2: Research
```bash
Read CLAUDE_DOCs/task_plan.md           # Refresh goals
WebSearch "morning exercise benefits"
Write CLAUDE_DOCs/notes.md              # Store findings
Edit CLAUDE_DOCs/task_plan.md           # Mark Phase 2 complete
```

### Loop 3: Synthesize
```bash
Read CLAUDE_DOCs/task_plan.md           # Refresh goals
Read CLAUDE_DOCs/notes.md               # Get findings
Write CLAUDE_DOCs/morning_exercise_summary.md
Edit CLAUDE_DOCs/task_plan.md           # Mark Phase 3 complete
```

### Loop 4: Deliver
```bash
Read CLAUDE_DOCs/task_plan.md           # Verify complete
Deliver CLAUDE_DOCs/morning_exercise_summary.md
```

---

## Example 2: Bug Fix Task

**User Request:** "Fix the login bug in the authentication module"

### CLAUDE_DOCs/task_plan.md
```markdown
# Task Plan: Fix Login Bug

## Goal
Identify and fix the bug preventing successful login.

## Phases
- [x] Phase 1: Understand the bug report ✓
- [x] Phase 2: Locate relevant code ✓
- [ ] Phase 3: Identify root cause (CURRENT)
- [ ] Phase 4: Implement fix
- [ ] Phase 5: Test and verify

## Key Questions
1. What error message appears?
2. Which file handles authentication?
3. What changed recently?

## Decisions Made
- Auth handler is in src/auth/login.ts
- Error occurs in validateToken() function

## Errors Encountered
- [Initial] TypeError: Cannot read property 'token' of undefined
  → Root cause: user object not awaited properly

## Status
**Currently in Phase 3** - Found root cause, preparing fix
```

---

## Example 3: Feature Development with Plan Change

**User Request:** "Add a dark mode toggle to the settings page"

### Initial Setup
```bash
Write CLAUDE_DOCs/task_plan.md
Write CLAUDE_DOCs/PLAN_TIMELINE/OVERALL.md
```

### Mid-task Plan Change (adding Phase 5)
```bash
# Before modifying phases, archive current plan
Copy CLAUDE_DOCs/task_plan.md → CLAUDE_DOCs/PLAN_TIMELINE/20260106_143000.md
Append to CLAUDE_DOCs/PLAN_TIMELINE/OVERALL.md:
  "| 20260106_143000 | Added Phase 5 for accessibility testing |"
Edit CLAUDE_DOCs/task_plan.md  # Add the new phase
```

### CLAUDE_DOCs/task_plan.md:
```markdown
# Task Plan: Dark Mode Toggle

## Goal
Add functional dark mode toggle to settings.

## Phases
- [x] Phase 1: Research existing theme system ✓
- [x] Phase 2: Design implementation approach ✓
- [ ] Phase 3: Implement toggle component (CURRENT)
- [ ] Phase 4: Add theme switching logic
- [ ] Phase 5: Accessibility testing (ADDED)
- [ ] Phase 6: Test and polish

## Decisions Made
- Using CSS custom properties for theme
- Storing preference in localStorage
- Toggle component in SettingsPage.tsx

## Status
**Currently in Phase 3** - Building toggle component
```

### CLAUDE_DOCs/notes.md:
```markdown
# Notes: Dark Mode Implementation

## Existing Theme System
- Located in: src/styles/theme.ts
- Uses: CSS custom properties
- Current themes: light only

## Files to Modify
1. src/styles/theme.ts - Add dark theme colors
2. src/components/SettingsPage.tsx - Add toggle
3. src/hooks/useTheme.ts - Create new hook
4. src/App.tsx - Wrap with ThemeProvider

## Color Decisions
- Dark background: #1a1a2e
- Dark surface: #16213e
- Dark text: #eaeaea
```

### CLAUDE_DOCs/PLAN_TIMELINE/OVERALL.md:
```markdown
# Plan Timeline

| Timestamp | Change Purpose |
|-----------|----------------|
| 20260106_140000 | Initial plan created |
| 20260106_143000 | Added Phase 5 for accessibility testing |
```

### CLAUDE_DOCs/dark_mode_implementation.md: (deliverable)
```markdown
# Dark Mode Implementation

## Changes Made

### 1. Added dark theme colors
File: src/styles/theme.ts
...

### 2. Created useTheme hook
File: src/hooks/useTheme.ts
...
```

---

## Example 4: Algorithm Development with Design Docs

**User Request:** "Design and implement a caching algorithm for our API"

### Create Design Document
```bash
Write CLAUDE_DOCs/Design/20260106_v1_算法设计.md
Append to CLAUDE_DOCs/Design/OVERALL.md:
  "| 20260106_v1_算法设计.md | LRU caching algorithm for API response optimization |"
```

### CLAUDE_DOCs/Design/20260106_v1_算法设计.md:
```markdown
# Algorithm Design: API Response Caching

## Problem Statement
API responses are slow due to repeated database queries.

## Proposed Solution
LRU (Least Recently Used) cache with TTL.

## Design Details
- Cache size: 1000 entries
- TTL: 5 minutes
- Eviction policy: LRU
- Data structure: HashMap + Doubly Linked List

## Pseudocode
...
```

### After Implementation - Create Results Analysis
```bash
Write CLAUDE_DOCs/ResultsAnalysis/20260106_v1_结果报告.md
Append to CLAUDE_DOCs/ResultsAnalysis/OVERALL.md:
  "| 20260106_v1_结果报告.md | Cache hit rate 87%, latency reduced by 65% |"
```

### CLAUDE_DOCs/ResultsAnalysis/20260106_v1_结果报告.md:
```markdown
# Results Report: API Caching v1

## Test Environment
- 10,000 requests over 1 hour
- 50 concurrent users

## Results
| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| Avg Latency | 450ms | 157ms | -65% |
| Cache Hit Rate | N/A | 87% | - |
| DB Queries/min | 2400 | 312 | -87% |

## Conclusion
LRU caching significantly improved API performance.
```

---

## Example 5: Error Recovery Pattern

When something fails, DON'T hide it:

### Before (Wrong)
```
Action: Read config.json
Error: File not found
Action: Read config.json  # Silent retry
Action: Read config.json  # Another retry
```

### After (Correct)
```
Action: Read config.json
Error: File not found

# Update CLAUDE_DOCs/task_plan.md:
## Errors Encountered
- config.json not found → Will create default config

Action: Write config.json (default config)
Action: Read config.json
Success!
```

---

## The Read-Before-Decide Pattern

**Always read your plan before major decisions:**

```
[Many tool calls have happened...]
[Context is getting long...]
[Original goal might be forgotten...]

→ Read CLAUDE_DOCs/task_plan.md   # This brings goals back into attention!
→ Now make the decision            # Goals are fresh in context
```

This is why Manus can handle ~50 tool calls without losing track. The plan file acts as a "goal refresh" mechanism.

---

## Complete Directory Structure Example

After a full development cycle, your `CLAUDE_DOCs/` might look like:

```
CLAUDE_DOCs/
├── task_plan.md                          # Current plan
├── notes.md                              # Research notes
├── api_caching_implementation.md         # Deliverable
│
├── PLAN_TIMELINE/
│   ├── OVERALL.md
│   ├── 20260106_100000.md               # Initial plan
│   ├── 20260106_143000.md               # Added testing phase
│   └── 20260107_091500.md               # Restructured for v2
│
├── Design/
│   ├── OVERALL.md
│   ├── 20260106_v1_算法设计.md
│   ├── 20260106_v1_架构设计.md
│   └── 20260107_v2_算法设计.md          # Optimized version
│
└── ResultsAnalysis/
    ├── OVERALL.md
    ├── 20260106_v1_结果报告.md
    └── 20260107_v2_结果分析.md           # Comparison analysis
```
