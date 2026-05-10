# claude-ai-workflows

> **Automated BDM + lead generation workflows** running daily — LinkedIn sweeps, Indeed MCP pipelines, cold outreach, and client acquisition funnels.

Part of [claude-ai-system](https://github.com/hmzainjamil/claude-ai-system).

---

## Overview

The HMZ AI workflow system runs autonomous business development and lead generation pipelines. Every workflow is scheduled, self-healing, and outputs structured data to Airtable/Notion/email.

---

## Active Workflow Categories

### BDM (Business Development) Sweeps

**LinkedIn BDM Sweep**
- Searches LinkedIn for high-ticket clients in target niches
- Filters: budget signals, job titles, company size, location
- Output: Qualified leads → Airtable CRM → personalized outreach sequence
- Schedule: Daily (configurable)
- Geo restrictions: Never India, Pakistan, Bangladesh, Philippines, Israel

**Indeed MCP Pipeline**
- Searches Indeed for freelance + contract opportunities
- Filters: $15+/hr or $500+ fixed price, 90+ buyer score, <48hr posted
- Platforms: LinkedIn + Indeed only (Upwork/Freelancer/PPH permanently removed)
- Output: Matched jobs → cover letter generated → application queued
- MCP: `anthropic-skills:client-hunting-indeed`

### Lead Generation Workflows

**Cold Email Outreach**
- Prospect research → personalized PDF audit → cold email + PDF attachment
- Each email includes: prospect's business name, city, brand palette
- Tools: Apollo MCP, Hunter.io, ReportLab PDF generator
- Output: Sent emails tracked in Airtable

**Google Ads Audit Pipeline**
- Scrapes prospect's Google Ads structure (via Playwright/Apify)
- Generates 11-page PDF audit (ReportLab, client brand palette from URL)
- Sends audit as lead magnet in cold email
- Skills: `ads-reporting` + `report-creator` + `ads-strategy`

**Reddit Lead Generation**
- Posts value-content threads in target subreddits
- Cap: 1 post per day MAX (account on bot-watch — never 2-3/day)
- Tracks engagement → DM qualified responders

### n8n Automation Workflows

8,159 workflow JSONs organized by integration:

| Category | Count | Top Workflows |
|---|---|---|
| Gmail/Email | ~874 | Cold outreach, follow-up sequences, inbox automation |
| Slack | ~328 | Lead alerts, team notifications, status updates |
| Telegram | ~309 | Bot responses, lead capture, CRM updates |
| AI/GPT/LLM | ~400+ | Content generation, lead scoring, research |
| CRM/Sales | ~121 | Apollo, HubSpot, Salesforce sync flows |
| LinkedIn | ~80+ | Profile scraping, connection automation |
| Google Sheets | ~200+ | Reporting, KPI tracking, data pipelines |
| Airtable | ~150+ | CRM, lead management, project tracking |
| Social Media | ~197 | Instagram, Twitter, Facebook automation |
| Ecommerce | ~82 | Shopify, WooCommerce, Stripe flows |
| SEO/Content | ~100+ | Blog auto-post, research collection |
| Data/Reporting | ~200+ | Dashboards, analytics, KPI flows |

See full manifest: [hmz-n8n-workflows](https://github.com/hmzainjamil/hmz-n8n-workflows)

---

## Workflow Output Formats

| Workflow | Output | Destination |
|---|---|---|
| BDM LinkedIn Sweep | Qualified lead list | Airtable CRM |
| Indeed Pipeline | Job matches + cover letters | Email queue |
| Cold Email Outreach | Sent email log | Airtable + Gmail |
| Google Ads Audit | 11-page PDF | Client email |
| Lead Gen Scrape | Structured data (JSON) | Airtable + Notion |
| n8n Automation | Varies by workflow | Configured destination |

---

## Daily Automation Schedule

| Time | Workflow | Output |
|---|---|---|
| 6:30 AM | github-sync | All repos pushed to GitHub |
| 7:00 AM | BDM LinkedIn Sweep | Fresh leads in Airtable |
| 7:30 AM | Indeed Pipeline | New job applications queued |
| 8:00 AM | Cold Email Outreach | Personalized emails sent |
| On-demand | Google Ads Audit PDF | Sent to prospect |
| On-demand | n8n workflow trigger | Webhook or manual |

---

## Platform Rules (Enforced Across All Workflows)

- **Geo blacklist:** India, Pakistan, Bangladesh, Philippines, Israel — never targeted
- **BDM platforms:** LinkedIn + Indeed ONLY (Upwork/Freelancer/PPH removed permanently)
- **Reddit:** Max 1 post/day (bot-watch active — never schedule 2-3/day)
- **Chrome sessions:** Always reuse persistent profile — never trigger re-login
- **File output:** Always to `~/Downloads/` — never Desktop

---

## Integration Stack

```
Apify MCP          → Web scraping, actor execution (zero Claude tokens)
Apollo MCP         → Lead enrichment, contact search, email sequences
Google Calendar    → Scheduling, event creation
Gmail MCP          → Email sending, thread search, draft creation
Slack MCP          → Team notifications, channel messaging
Notion MCP         → Lead tracking, project management
Airtable MCP       → CRM, structured data storage
n8n (8,159 flows)  → Workflow automation layer
```

---

## Full System

[claude-ai-system](https://github.com/hmzainjamil/claude-ai-system) | [claude-ai-skills](https://github.com/hmzainjamil/claude-ai-skills) | [claude-ai-agents](https://github.com/hmzainjamil/claude-ai-agents) | [claude-ai-automations](https://github.com/hmzainjamil/claude-ai-automations)

---

*Auto-updated daily by github-sync at 6:30 AM — HMZ AI Agency*
