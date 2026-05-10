# claude-ai-workflows

> **HMZ automated workflow definitions** — BDM sweeps, lead pipelines, LinkedIn/Indeed scrapers, and daily automation configs.

Part of the [HMZ AI System](https://github.com/hmzainjamil/claude-ai-system).

## Active Workflows

| Workflow | Schedule | Output |
|---|---|---|
| **BDM Morning Sweep** | 7:00 AM daily | LinkedIn + Indeed leads → HTML report |
| **BDM Evening Sweep** | Evening | End-of-day refresh |
| **Elite Leads** | 6:00 AM daily | Top 50 prospects → Excel |
| **GitHub Sync** | 6:30 AM daily | All repos pushed |

## Output Files

```
~/Downloads/HMZ-BDM-Morning-YYYY-MM-DD.html
~/Downloads/HMZ-BDM-Evening-YYYY-MM-DD.html
~/Downloads/HMZ-Elite-Leads-YYYY-MM-DD.xlsx
```

## n8n Workflows

8,159 additional n8n workflows: [hmz-n8n-workflows](https://github.com/hmzainjamil/hmz-n8n-workflows)

**Main repo → [claude-ai-system](https://github.com/hmzainjamil/claude-ai-system)**
