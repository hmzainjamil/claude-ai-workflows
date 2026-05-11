# claude-ai-workflows

> **Production Claude Code workflow library — multi-step automated pipelines connecting hooks, skills, scripts, Paperclip API, and Composio for DigiMinds agency operations**

[![workflows](https://img.shields.io/badge/workflows-12_production-blue?style=flat)](.) [![triggers](https://img.shields.io/badge/triggers-hooks_launchagent_cron_cli-green?style=flat)](.) [![model](https://img.shields.io/badge/model-tier0_zero_claude_tokens-orange?style=flat)](.) [![company](https://img.shields.io/badge/company-DigiMinds-red?style=flat)](.)

[Overview](#overview) · [Workflows](#workflows) · [Architecture](#architecture) · [Triggers](#triggers) · [Config](#config) · [Tips](#tips) · [Gotchas](#gotchas)

---

## 🧠 OVERVIEW

Multi-step workflow definitions for Claude Code that chain together hooks, skills, MCP tools, Paperclip API calls, and Composio integrations into fully automated pipelines. Every workflow runs on Tier 0 models (zero Claude tokens for sub-tasks) and logs to `~/Library/Logs/`.

| Component | Value |
|---|---|
| Company | DigiMinds (digiminds.org) |
| Paperclip API | `http://127.0.0.1:3100/api` |
| Composio | 200+ external tool connections |
| Model routing | G0DM0D3 Tier 0 (Groq → Gemini → DeepSeek → Ollama) |
| Log location | `~/Library/Logs/` |
| Config | `~/.claude/settings.json` (hooks) + `~/Library/LaunchAgents/` (daemons) |

---

## ⚙️ WORKFLOW INVENTORY

| Workflow | Trigger | Steps | Output | Model |
|---|---|---|---|---|
| Cold Email + PDF | Daily 9AM / manual | Scrape → Score → Write email → Generate PDF → Send | Email + branded PDF per prospect | GPT-4o-mini |
| 360° Audit Generator | Manual CLI | URL → Brand colors → Sections → 11-page PDF | Client audit PDF (~40 pages) | Gemini Flash |
| Lead Enrichment | Daily 7:30 AM | Apollo → Enrich → ICP score → CRM | Qualified lead list (80+ score) | Groq Llama 3 |
| LinkedIn Publisher | Daily 8 AM | Trends → Angle → Generate → Quality gate → Schedule | LinkedIn post (10 AM target) | Gemini Flash |
| KPI Scorecard | Daily 6 PM | Pull metrics → Calculate variance → Score → Alert | 28-KPI JSON scorecard | Groq Llama 3 |
| CEO Review Loop | Every 6h | Goals → Agents → Tasks → Decide → Log | Decision log → Paperclip API | Tier 0 mix |
| Competitor Intel | Daily 10 AM | Ad library → LinkedIn → Clutch → Diff → Brief | Intel brief → CEO loop | Apify + Groq |
| GitHub Portfolio Sync | Daily 6:30 AM | Skills → Agents → Scripts → Commit → Push | Updated claude-ai-system repo | Shell |
| Skill Auto-Activate | Every prompt | Keyword match → skill-on → context inject | Active skill set for session | Rules-based |
| BDM Lead Sweep | Mon/Wed/Fri 9 AM | LinkedIn search → Score → CRM → Draft outreach | 3-5 hot leads + drafts | GPT-4o-mini |
| Paperclip Health Check | Every 15 min | API ping → Daemon check → Agent status | Health report → alert if down | Shell |
| Trends + Content Sync | Mon/Wed/Fri 6 AM | Trends scan → Content calendar → Generate backlog | 3 posts queued | Gemini Flash |

---

## 🔧 ARCHITECTURE

```
┌─────────────────────────────────────────────────────┐
│            WORKFLOW EXECUTION STACK                 │
└─────────────────┬───────────────────────────────────┘
                  │
    ┌─────────────┴──────────────┐
    ▼                            ▼
LaunchAgent daemons        Hook triggers (settings.json)
(scheduled, always-on)     (UserPromptSubmit, PostToolUse)
    │                            │
    └──────────┬─────────────────┘
               ▼
    Workflow scripts (~/.claude/bin/)
               │
    ┌──────────┼──────────┐
    ▼          ▼          ▼
Tier 0       Apify     Composio
Models      actors     tools (200+)
(Groq,      (scrape)   (Slack, GitHub,
Gemini,                Apollo, LinkedIn)
DeepSeek)
    │
    ▼
Paperclip API (port 3100) — state, decisions, logs
```

| Layer | Component | Location |
|---|---|---|
| Orchestrator | Claude Code | CLI session |
| Scheduler | LaunchAgent daemons | ~/Library/LaunchAgents/ |
| Hook layer | settings.json hooks | ~/.claude/settings.json |
| Scripts | bin/ scripts | ~/.claude/bin/ |
| Models | G0DM0D3 routing | Tier 0 first |
| Scraping | Apify actors | apify.com |
| External tools | Composio | ~/.composio/ |
| State/decisions | Paperclip API | port 3100 |
| Logs | System logs | ~/Library/Logs/ |

---

## ⚡ TRIGGER TYPES

| Trigger | How | Example |
|---|---|---|
| LaunchAgent cron | `StartCalendarInterval` in plist | Daily 7:30 AM lead engine |
| UserPromptSubmit hook | `settings.json` hooks | Skill auto-activate on every prompt |
| PostToolUse hook | `settings.json` hooks | Auto-commit after file write |
| PreToolUse hook | `settings.json` hooks | Tier 0 routing enforcement |
| Manual CLI | `~/.claude/bin/<script>` | `~/.claude/bin/paperclip-lead-engine` |
| Webhook | Paperclip API POST | Lead scored 80+ → blink alert |
| fswatch | File system events | New file → auto-push to GitHub |

---

## 🔩 HOOK CONFIG (settings.json)

```json
{
  "hooks": {
    "UserPromptSubmit": [
      {
        "matcher": ".*",
        "hooks": [
          {"type": "command", "command": "~/.claude/bin/skill-auto-activate"},
          {"type": "command", "command": "~/.claude/bin/tier0-prompt-inject"}
        ]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {"type": "command", "command": "~/.claude/bin/auto-learn"}
        ]
      }
    ],
    "Stop": [
      {
        "matcher": ".*",
        "hooks": [
          {"type": "command", "command": "~/.claude/bin/session-queue-processor"}
        ]
      }
    ]
  }
}
```

---

## 💡 TIPS

■ **Workflow Design (6)**
| Tip | Source |
|---|---|
| Every workflow step must be idempotent — safe to re-run without side effects | Design principle |
| Use Tier 0 for all LLM calls inside workflows — never Claude for sub-tasks | G0DM0D3 mandate |
| Log every workflow step: `echo "[workflow] step completed" >> ~/Library/Logs/x.log` | Ops rule |
| Workflows touching external APIs must have retry logic with exponential backoff | Error handling |
| Test with `--dry-run` flag before first production run | Safety rule |
| Idempotency key: use timestamp+hash to deduplicate repeated triggers | Design |

■ **Trigger Management (4)**
| Tip | Source |
|---|---|
| LaunchAgent `KeepAlive=true` + `RunAtLoad=true` for always-on workflows | plist config |
| `StartCalendarInterval` is more reliable than cron on macOS | macOS SOP |
| Verify LaunchAgent loaded: `launchctl list | grep ai.hmz` | Debug |
| Hook order matters: skill-auto-activate must run before tier0-prompt-inject | Hook sequencing |

■ **Integration (4)**
| Tip | Source |
|---|---|
| Paperclip API at port 3100 = single source of truth for all workflow state | Architecture |
| Composio handles all OAuth — never store tokens in workflow scripts | Security |
| Apify actors handle all web scraping — never raw requests in workflows | Tool routing |
| Workflows report back to CEO loop via POST /api/decisions | CEO integration |

■ **Debugging (4)**
| Tip | Source |
|---|---|
| LaunchAgent exit=256 = script returned exit 1 — check `-error.log` | Debug SOP |
| `launchctl start ai.hmz.<name>` to test-trigger without waiting for schedule | Debug |
| All workflow logs in `~/Library/Logs/` — one file per workflow | Log location |
| Add `set -x` to shell scripts for verbose debugging during development | Shell debug |

---

## ☠️ TOOLS REPLACED

| Claude Workflows | Replaced |
|---|---|
| Automated multi-step pipelines | Manual step-by-step execution (30-90 min each) |
| Hook-triggered automation | Remembering to run scripts manually |
| Tier 0 model routing | Burning Claude quota on every workflow step |
| State management via Paperclip API | Losing workflow state between steps |
| LaunchAgent scheduling | Fragile cron jobs that die on system sleep |
| Composio external tool calls | Building OAuth integrations per service |
| Apify scraping actors | Brittle Playwright/BeautifulSoup scrapers |
| Auto-logging | Discovering failures only when clients complain |

---

## ⚠️ GOTCHAS

| Issue | Fix |
|---|---|
| Hook not firing | Verify `settings.json` hook syntax + check hook logs |
| LaunchAgent exit=256 | Script returned error — check `~/Library/Logs/<name>-error.log` |
| Workflow ran but no output | Check Paperclip API at port 3100 — may be down |
| Tier 0 model unavailable | Fallback defined in each workflow — check G0DM0D3 config |
| Composio auth expired | `composio add <service>` to re-authenticate |
| Duplicate workflow runs | Add mutex lock: `[ -f /tmp/workflow.lock ] && exit 0` |
| Workflow slower than expected | Check if Ollama is loaded — may be using disk not GPU |
| API rate limit in workflow | Add `sleep 1` between calls — Composio has per-service limits |

---

## 🚀 QUICK REFERENCE

```bash
# List all LaunchAgent workflows
launchctl list | grep ai.hmz

# Trigger workflow manually
~/.claude/bin/paperclip-lead-engine
~/.claude/bin/paperclip-content-engine

# Check workflow logs
tail -f ~/Library/Logs/paperclip-lead-engine.log

# Test hook firing
~/.claude/bin/skill-auto-activate <<< "google ads ppc campaign"

# Check Paperclip workflow state
curl http://127.0.0.1:3100/api/decisions?date=today | jq '.'
```

---

*Part of [DigiMinds AI Agency Stack](https://github.com/hmzainjamil) — Claude Code workflow automation library*
