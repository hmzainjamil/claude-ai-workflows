<p align="center">
  <img src="https://img.shields.io/badge/HMZ-WORKFLOWS-15C1E6?style=for-the-badge&logoColor=white" alt="HMZ Workflows" height="60">
</p>

<h1 align="center">Claude AI Workflows</h1>

<p align="center">
  <strong>Production AI automation workflows — multi-agent pipelines, Claude Code skill chains, and LaunchAgent-powered scheduled tasks</strong>
</p>

<p align="center">
  <a href="https://github.com/hmzainjamil"><img src="https://img.shields.io/badge/By-HMZ-6C3EE8?style=for-the-badge" alt="By HMZ"></a>
  <a href="#workflows"><img src="https://img.shields.io/badge/Workflows-50%2B-20A34E?style=for-the-badge" alt="50+ Workflows"></a>
  <a href="#"><img src="https://img.shields.io/badge/Multi--Agent-Enabled-F86606?style=for-the-badge" alt="Multi-Agent"></a>
  <a href="#"><img src="https://img.shields.io/badge/n8n-8%2C000%2B-246DFF?style=for-the-badge" alt="n8n"></a>
</p>

<p align="center">
  <a href="#overview">Overview</a> &bull;
  <a href="#workflows">Workflows</a> &bull;
  <a href="#quick-start">Quick Start</a> &bull;
  <a href="#use-cases">Use Cases</a> &bull;
  <a href="#installation">Installation</a> &bull;
  <a href="#resources">Resources</a>
</p>

---

## Overview

**Claude AI Workflows** documents the complete set of multi-agent and automation workflows running inside the HMZ AI system. These are not n8n JSON files — these are **meta-workflows**: Claude Code skill chains, agent orchestration patterns, and LaunchAgent-managed pipelines that combine multiple AI models, MCP tools, and external APIs into production-grade outcomes.

Three categories of workflows:

1. **Agent orchestration workflows** — how the 210 agents coordinate on complex tasks
2. **Skill chain workflows** — how skills compose (e.g. `ads-strategy → ads-creative → ads-copy → market-launch`)
3. **Scheduled pipeline workflows** — LaunchAgent-triggered daily/weekly automation chains

---

## Workflows

### Lead Generation Pipeline
```
Vibe Prospecting MCP → Apollo MCP enrichment → Python/openpyxl Excel formatter → Mailchimp CSV export
Trigger: "Find [N] [business type] in [city]"
Output: Excel with name, phone, email, website, Instagram, Facebook, Google rating, reviews
Time: ~3 minutes for 50 leads
```

### Paid Media Audit Pipeline
```
Google Ads MCP → Meta Ads MCP → Paid Media Auditor agent → ReportLab PDF → ~/Downloads/
Trigger: "Audit my Google Ads / Meta Ads"
Output: 11-page PDF audit with ROAS, wasted spend, creative fatigue, recommendations
Time: ~8 minutes
```

### Content Production Pipeline
```
SEO Specialist → keyword cluster → Content Creator → market-copy skill → market-social skill → draft → Canva/Figma
Trigger: "Create content plan for [domain] targeting [keywords]"
Output: Editorial calendar + 10 drafted posts + social variants
Time: ~15 minutes
```

### Cold Outreach Pipeline
```
Outbound Strategist → ICP definition → Apollo prospecting → Email Intelligence Engineer → 7-email sequence → Mailchimp CSV
Trigger: "Build cold outreach campaign for [service] targeting [ICP]"
Output: Segmented prospect list + personalized email sequence ready to import
Time: ~20 minutes
```

### GitHub Daily Sync Pipeline
```
LaunchAgent (6:30 AM) → github-sync → skills sync → agents sync → n8n manifest rebuild → credential scrub → git push → README audit → new repo discovery
Trigger: Daily at 6:30 AM (automatic)
Output: claude-ai-system GitHub repo fully updated
Time: ~2 minutes
```

### Multi-LLM Burst Workflow
```
User prompt → skill-auto-activate hook → llm-burst → [Groq + Gemini + DeepSeek + GPT4All + Kimi K2 fire in parallel] → judge scoring → winner synthesis → Claude final output
Trigger: Every prompt (automatic)
Savings: 75–95% Claude token reduction vs direct Claude calls
Time: +0.3s overhead, often faster due to parallelism
```

### UGC Ad Production Pipeline
```
Brief → Kimi 8K script writer (20 scripts) → Actor matcher → Arcads API parallel render → MP4s in ~/ugc-output/
Trigger: "Generate 20 UGC ads for [product]"
Output: 20 MP4 video ads named by hook type
Time: ~45 minutes (parallel render)
Cost: ~just per ad at just,500/mo tool cost → 90% gross margin
```

---

## Quick Start

```bash
# Trigger the lead gen pipeline
"Find top 30 chiropractors in Dallas — phone, email, Instagram, Google rating. Export Excel."

# Trigger the paid media audit
"Full audit of my Meta Ads account — last 30 days ROAS by campaign, wasted spend, creative fatigue"

# Trigger multi-LLM burst manually
~/.claude/bin/llm-burst "Write positioning copy for my AI agency targeting e-com brands"

# Trigger the content pipeline
"Build a 30-day content calendar for [domain] targeting [keywords] — LinkedIn + Twitter + blog"

# Run the full daily sync manually
~/.claude/bin/github-sync
```

---

## Use Cases

| Workflow | Time | Output |
|---|---|---|
| Lead gen (50 leads) | ~3 min | Excel with 11 columns per lead |
| Paid media audit | ~8 min | 11-page PDF report |
| Content calendar | ~15 min | 30 posts + social variants |
| Cold outreach campaign | ~20 min | Prospect list + 7-email sequence |
| UGC ad batch (20 ads) | ~45 min | 20 MP4 video ads |
| Technical SEO audit | ~10 min | Full audit report + fix checklist |
| Competitor analysis | ~12 min | Positioning gaps + opportunity matrix |
| Full GTM strategy | ~30 min | ICP + messaging + channels + 90-day calendar |

---

## Installation

```bash
git clone https://github.com/hmzainjamil/claude-ai-workflows.git

# These workflows require the full HMZ skill stack:
git clone https://github.com/hmzainjamil/claude-ai-skills.git ~/.claude/skills
git clone https://github.com/hmzainjamil/claude-ai-agents.git ~/.claude/agents
```

---

## Resources

- **[claude-ai-system](https://github.com/hmzainjamil/claude-ai-system)** — Full HMZ system
- **[hmz-n8n-workflows](https://github.com/hmzainjamil/hmz-n8n-workflows)** — 8,000+ n8n workflows
- **[claude-ai-automations](https://github.com/hmzainjamil/claude-ai-automations)** — Scripts powering these workflows

## License

MIT

---

<p align="center">Built by <a href="https://github.com/hmzainjamil">Hafiz Muhammad Zulqarnain</a> &mdash; HMZ AI Agency</p>