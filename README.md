# claude-ai-workflows

> **Production Claude Code workflows — multi-step automated pipelines for DigiMinds agency operations**

[![workflows](https://img.shields.io/badge/workflows-production-blue?style=flat)](.) [![automation](https://img.shields.io/badge/type-automation-green?style=flat)](.) [![company](https://img.shields.io/badge/company-DigiMinds-orange?style=flat)](.)

[Overview](#overview) · [Workflows](#workflows) · [Architecture](#architecture) · [Tips](#tips)

---

## 🧠 OVERVIEW

Production multi-step workflow definitions for Claude Code — combining hooks, skills, scripts, and Paperclip API calls into automated pipelines. These workflows handle everything from audit PDF generation to lead qualification to content publishing.

| Component | Value |
|---|---|
| Trigger types | Hooks, LaunchAgent, cron, manual CLI |
| Integration | Paperclip API, Composio, MCP servers |
| Model routing | Tier 0 (Groq/Gemini/Ollama) — zero Claude tokens |
| Output | PDFs, CRM entries, LinkedIn posts, audit reports |

---

## ⚙️ WORKFLOW INVENTORY

| Workflow | Trigger | Steps | Output |
|---|---|---|---|
| Cold Email + PDF | Manual/Cron | Scrape → Score → Generate PDF → Send | Per-prospect PDF + email |
| Audit Generator | Manual | URL → Brand colors → 11-page PDF | Client audit PDF |
| Lead Enrichment | Daily 7:30 AM | Apollo → Enrich → Score → CRM | Qualified lead list |
| LinkedIn Publisher | Daily 8 AM | Trends → Generate → Quality check → Schedule | LinkedIn post |
| KPI Report | Daily 6 PM | Collect → Calculate → Score → Alert | KPI scorecard |
| CEO Loop | Every 6h | Goals → Review → Decide → Log | Decision log |

---

## 💡 TIPS

■ **Workflow Design (5)**
| Tip | Source |
|---|---|
| Every workflow step must be idempotent — safe to re-run | Design principle |
| Use Tier 0 routing for all LLM calls inside workflows | G0DM0D3 mandate |
| Log every step output to `~/Library/Logs/` for debugging | Ops rule |
| Workflows that touch external APIs need retry logic | Error handling |
| Test workflows with dry-run flag before production use | Dev workflow |

■ **Integration (3)**
| Tip | Source |
|---|---|
| Paperclip API at port 3100 is the central hub for workflow state | Architecture |
| Composio handles all OAuth to external services | Auth layer |
| Apify actors handle all web scraping — never scrape with raw requests | Tool routing |

---

## ☠️ TOOLS REPLACED

| Claude Workflows | Replaced |
|---|---|
| Automated multi-step pipelines | Manual step-by-step execution |
| Reliable workflow execution | Fragile shell scripts |
| State management | Forgetting where a workflow left off |

---

*Part of [DigiMinds AI Agency Stack](https://github.com/hmzainjamil)*
