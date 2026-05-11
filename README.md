# claude-ai-workflows

![Claude Code](https://img.shields.io/badge/Claude_Code-workflow_patterns-blue?style=flat&labelColor=000) ![OODA](https://img.shields.io/badge/framework-OODA_loop-orange?style=flat&labelColor=555) ![Multi-agent](https://img.shields.io/badge/pattern-multi--agent_orchestration-purple?style=flat&labelColor=555) ![Status](https://img.shields.io/badge/status-production-green?style=flat&labelColor=555)

Production Claude Code workflow patterns — orchestration blueprints, multi-agent coordination, scheduled task design, and OODA-driven decision frameworks. Not tutorials. Real patterns running 24/7 in the DigiMinds agency stack.

## 🧠 WHAT THIS IS

A workflow library for Claude Code power users. Each pattern solves a specific coordination challenge: how to parallelize tasks without blowing the context window, how to chain agents without losing state, how to run autonomous loops that self-correct.

| Pattern | File | Use Case |
|---|---|---|
| Parallel Research | `parallel-research.md` | Fan out to 5+ agents, synthesize results in one final call |
| Sequential Pipeline | `sequential-pipeline.md` | A→B→C chains where each step depends on previous output |
| Autonomous Loop | `autonomous-loop.md` | Self-running agents that monitor, decide, and act on schedule |
| Worktree Isolation | `worktree-isolation.md` | Agent isolation with `--isolation worktree` for safe parallel edits |
| Context Guard | `context-guard.md` | Prevent context overflow in long sessions |
| OODA Sprint | `ooda-sprint.md` | Rapid decision-execute cycle for time-sensitive tasks |

## ⚙️ CORE PATTERNS

**Parallel Research (fan-out → synthesize):**
```
Agent Tool (3x simultaneous)
├── Explore agent: "find all API endpoints"
├── Explore agent: "find all database schemas"
└── Explore agent: "find all auth implementations"
    ↓ (all 3 complete)
Sonnet: synthesize findings → single coherent report
```
Token cost: 3 × Tier-0-agent cost. Zero Claude tokens for research phase.

**Autonomous Loop (scheduled + self-correcting):**
```
Scheduled Task (cron: 0 */6 * * *)
  1. Pull current state (Paperclip API / GA4 / CRM)
  2. Compare to targets (KPI thresholds)
  3. Decision tree: OK → log; MISS → create corrective task; CRITICAL → alert
  4. Write decisions to ~/.paperclip/ceo-decisions.log
  5. Sleep until next cron fire
```

**Worktree Isolation:**
```bash
# Agent operates on isolated git branch — no conflict with main
Agent(isolation: "worktree") {
  task: "refactor auth module"
  # → creates temp branch, edits files there
  # → if changes made: returns worktree path + branch name
  # → if no changes: worktree auto-cleaned
}
```

## 💡 SCHEDULED TASK PATTERNS

DigiMinds runs 6 autonomous scheduled agents:

| Agent | Schedule | What It Does |
|---|---|---|
| CEO Strategy Loop | Every 6h | Pulls state, creates 3+ tasks, hires agents for skill gaps |
| Lead Enrichment Engine | 7:30 AM daily | Sources 10+ leads, scores, enriches, creates BDM tasks |
| LinkedIn Content Engine | 8:00 AM daily | Trending topic → LinkedIn post → saves to ~/Downloads/ |
| Competitor Intel | 10:00 AM daily | Monitors competitor pricing, generates 3 strategic recs |
| KPI Health Monitor | 6:00 PM daily | KPI audit, auto-creates corrective tasks for misses |
| Market Trends Scanner | Mon/Wed/Fri 6 AM | 8-topic trend scan, creates opportunity tasks |

All scheduled via `mcp__scheduled-tasks__create_scheduled_task` — run remotely even when machine is off.

## 🔧 WORKFLOW DESIGN RULES

1. **Context budget:** Plan before running. Each sub-agent = context cost. Fan out to Tier 0 models, not Claude.
2. **State hand-off:** Never pass entire context between agents. Extract only the facts the next agent needs.
3. **Idempotency:** Every workflow must be safe to re-run. No side effects on re-execution.
4. **Failure isolation:** One agent failing should not kill the pipeline. Design fallback paths.
5. **Output contracts:** Define expected output schema before building the agent. Test the schema first.

## ☠️ ANTI-PATTERNS

| Anti-pattern | Problem | Fix |
|---|---|---|
| "Ask Claude to do everything" | Context overflow, high token cost | Fan out to Tier 0 agents |
| Sequential when parallel is possible | Slow, no throughput gain | Identify independent steps, parallelize |
| Passing full files between agents | Context explosion | Extract diffs only |
| No idempotency | Re-run breaks state | Add existence checks before writes |
| Long autonomous loops without state save | Context lost on compaction | Write state to file after each loop iteration |
