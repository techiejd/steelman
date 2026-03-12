# parallel-resource-isolation

A Claude Code skill that proactively detects and resolves resource conflicts when multiple Claude instances work on the same project in parallel.

## Problem

When two or more Claudes run simultaneously (e.g., in different worktrees), they collide on:

- **Ports** — both try to start a dev server on :3000, one fails and kills the other's process
- **Databases** — both write test data and assert on counts, getting each other's rows
- **Playwright browsers** — both fight over the same browser lock/temp directory, causing hangs

## Solution

Pure Scout approach — each Claude observes system state, silently adapts, and reports what it chose. No coordination files, no lock files, no shared state.

| Resource | Detection | Adaptation | Cleanup |
|----------|-----------|------------|---------|
| Dev server port | `lsof -i :<port>` | `PORT=<next_free>` | None |
| Supabase DB | Check if tests write/assert | `parallel_<epoch>_` schema | Drop schema after tests |
| Playwright browser | Check for lock contention | `TMPDIR` or `PLAYWRIGHT_BROWSERS_PATH` | Auto-cleaned |

## Example Output

```
⚡ Parallel isolation:
  Dev server: port 3003 (3000, 3001, 3002 were in use)
  DB schema: parallel_1741234567_
  Playwright: /tmp/playwright_1741234567
```

## Stack

Built for Next.js + Supabase + Playwright. Can be extended to other stacks.

## TDD Test Results

Tested with subagent pressure scenarios across RED/GREEN/REFACTOR cycles.

- **Baseline (no skill): ~40%** — agents don't kill processes but use wrong DB strategy, no reporting, no proactive detection
- **With skill: 100%** — all behaviors correct across port, DB, and Playwright isolation
