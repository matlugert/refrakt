# Sample Refrakt Output

> This is an example of what `/refrakt` produces when run against a hypothetical task management CLI tool.

---

## 1. Capability Map

- **Core function**: CLI task manager with local SQLite storage, supporting create/read/update/delete operations on tasks with tags, priorities, and due dates
- **Stack**: Node.js + TypeScript, Commander.js for CLI, better-sqlite3 for storage, chalk for terminal output
- **Active frontier**: Recent commits added recurring task support and a `sync` command stub (not yet implemented)
- **Data model**: Rich task schema with tags (many-to-many), projects, time estimates, and completion history
- **Output system**: Pluggable formatters (table, JSON, CSV) with a `Formatter` interface
- **Gap**: Completion history is stored but never surfaced — no analytics or reporting
- **Gap**: The `sync` command exists as a stub with an interface but no implementation
- **Underutilized**: Tag system supports hierarchical tags (`work/meetings`) but no commands use hierarchy

## 2. Candidate Table

| # | Title | Lev | Feas | Wow | Comp | Evid | Total |
|---|-------|-----|------|-----|------|------|-------|
| 1 | Velocity Dashboard | 4 | 5 | 3 | 5 | 5 | **22** |
| 2 | Smart Scheduling via History Patterns | 4 | 3 | 5 | 4 | 3 | **19** |
| 3 | Natural Language Task Capture | 3 | 3 | 4 | 3 | 3 | **16** |
| 4 | Tag-Aware Time Budgets | 3 | 4 | 3 | 4 | 4 | **18** |
| 5 | Git-Based Sync Engine | 3 | 4 | 2 | 2 | 4 | **15** |

**[1] Velocity Dashboard**
Pitch: Surface the completion history data that's already being collected but never shown. Give users a terminal-rendered productivity dashboard showing tasks completed per day/week, average completion time by tag, and streak tracking — turning a task list into a personal productivity system.

**[2] Smart Scheduling via History Patterns**
Pitch: Analyze historical completion patterns (time-of-day, day-of-week, tag correlations) to suggest optimal scheduling. "You complete `work/deep` tasks 2.3x faster before noon."

**[3] Natural Language Task Capture**
Pitch: Parse natural language input ("meet Sarah about budget Thursday 2pm #work/meetings") into structured task fields using a local rule-based parser (no API dependency).

**[4] Tag-Aware Time Budgets**
Pitch: Set weekly time budgets per tag hierarchy ("max 10h on work/meetings") and get warnings when approaching limits — turns tags from labels into a time management framework.

**[5] Git-Based Sync Engine**
Pitch: Implement the existing `sync` stub using git as the transport — commit SQLite changes to a bare repo for cross-device sync without a server.

## 3. Critique Delta

- **[1] Velocity Dashboard**: 20 → 22. Sharpened mechanism from "show stats" to specific visualizations using the existing Formatter interface. Evidence confidence jumped from 3→5 after confirming `completion_history` table schema.
- **[2] Smart Scheduling**: 18 → 19. Reduced scope from ML model to simple statistical patterns. Still uncertain about minimum data threshold for useful suggestions.
- **[3] NL Capture**: 17 → 16. Critique revealed the parser complexity is higher than pitched. Chrono.js dependency pushes feasibility down. Replaced "AI-powered" framing with rule-based approach.
- **[4] Tag Budgets**: 16 → 18. Added concrete mechanism: `time_estimate` field already exists, hierarchical tags already parsed. Compounding value increased — makes both tags AND time estimates more useful.
- **[5] Git Sync**: 14 → 15. Narrowed from "generic sync" to git-specific. Lower wow-factor (many tools do this) but highly feasible given the existing stub.

## 4. Evidence Ledger

### [1] Velocity Dashboard — PASS
| Anchor | Proves |
|--------|--------|
| `src/db/schema.ts:42-58` — `completion_history` table with `completed_at`, `time_spent`, `tag_ids` | Rich historical data already being collected |
| `src/formatters/index.ts` — `Formatter` interface with `render(data)` method | Pluggable output system; dashboard is a new formatter |
| `src/commands/list.ts:89` — tag aggregation query already groups by tag hierarchy | Hierarchical grouping logic exists and is tested |
| `src/utils/date.ts` — date range utilities (week boundaries, day-of-week) | Date bucketing for dashboard periods already available |
- Unresolved deps: Terminal chart library (nice-to-have, can use ASCII art initially)
- **PASS** — 4 anchors, 0 critical deps

### [2] Smart Scheduling — FAIL
| Anchor | Proves |
|--------|--------|
| `src/db/schema.ts:42-58` — completion history | Historical data exists |
| `src/commands/schedule.ts` — scheduling command | Command structure exists |
- Unresolved deps: Statistical analysis library, minimum data threshold unclear
- **FAIL** — Only 2 anchors, data threshold is a critical unknown

### [3] NL Capture — FAIL
| Anchor | Proves |
|--------|--------|
| `src/commands/add.ts` — task creation command | Entry point exists |
| `src/models/task.ts` — task schema | Target data model is defined |
| `src/utils/tags.ts` — tag parser | Tag parsing exists |
- Unresolved deps: chrono-node or custom date parser (critical — no date parsing exists in the project)
- **FAIL** — 3 anchors but 1 critical dependency (date parsing)

### [4] Tag Budgets — PASS
| Anchor | Proves |
|--------|--------|
| `src/utils/tags.ts:23` — `parseHierarchy()` splits `work/meetings` into levels | Hierarchical tag support already works |
| `src/db/schema.ts:31` — `time_estimate` field on tasks | Time data already structured per task |
| `src/commands/list.ts:89` — tag aggregation query | Can sum time per tag hierarchy level |
| `src/config.ts` — user config file with `settings` object | Place to store budget thresholds |
- Unresolved deps: None critical (warning display is a minor UI addition)
- **PASS** — 4 anchors, 0 critical deps

### [5] Git Sync — PASS
| Anchor | Proves |
|--------|--------|
| `src/commands/sync.ts` — stub with `SyncProvider` interface | Architecture is already designed |
| `src/db/export.ts` — SQLite export/import utilities | Data serialization exists |
| `package.json` — `simple-git` already in dependencies | Git operations library already available |
- Unresolved deps: Conflict resolution strategy (non-critical for v1, last-write-wins is acceptable)
- **PASS** — 3 anchors, 0 critical deps

## 5. Winner

**[1] Velocity Dashboard** (22/25)

Highest-scoring eligible candidate. It uniquely compounds value across the _entire_ project — completion history, tags, time estimates, and the formatter system all become more valuable. The evidence gate is the strongest of any candidate, with 4 well-connected anchors and zero critical dependencies.

## 6. Implementation Blueprint

### Files to create/modify

| Action | Path | Purpose |
|--------|------|---------|
| Create | `src/formatters/dashboard.ts` | New `DashboardFormatter` implementing `Formatter` interface |
| Create | `src/commands/dashboard.ts` | New `/dashboard` command with period flags |
| Modify | `src/commands/index.ts` | Register dashboard command |
| Create | `src/analytics/velocity.ts` | Query functions for completion metrics |
| Modify | `src/db/queries.ts` | Add `getCompletionsByPeriod()` and `getVelocityByTag()` |

### Interface changes

```typescript
// src/analytics/velocity.ts
interface VelocityMetrics {
  period: 'day' | 'week' | 'month';
  tasksCompleted: number;
  avgCompletionTime: number; // minutes
  byTag: Map<string, { count: number; avgTime: number }>;
  streak: { current: number; longest: number };
}

function getVelocity(period: DateRange): VelocityMetrics;
function getStreak(asOf?: Date): { current: number; longest: number };
```

### Data flow

1. User runs `tasks dashboard [--period week|month|all]`
2. `DashboardCommand` calls `getVelocity(period)` and `getStreak()`
3. Analytics module queries `completion_history` joined with `tags`
4. Results passed to `DashboardFormatter.render(metrics)`
5. Formatter outputs ASCII chart + summary table to terminal

### Edge cases

1. **No completion history**: Show "Complete some tasks first" with a getting-started hint, not an empty chart
2. **Single tag dominance**: If >80% of tasks share one tag, show "tip: try more specific tags for better insights"
3. **Time estimate missing**: Exclude from avg completion time calculation, show "N tasks without estimates" footnote

### Rollout plan

1. **First**: `velocity.ts` analytics module + unit tests (pure functions, easy to test)
2. **Second**: `dashboard.ts` command with basic table output (no charts yet)
3. **Third**: ASCII chart rendering in `DashboardFormatter`
4. **Validate**: Run against own task database, screenshot output for review

### Estimated scope: **M** (1-2 days)
