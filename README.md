# Claude AI Workflows

A small collection of Claude Code skill instructions for recurring job-search and lead-research workflows. Despite the repository name, these files are prompts and operating procedures; this repository does not contain a verified scheduler, n8n deployment, or end-to-end automation runtime.

## Contents

| Folder | Purpose stated by its skill file |
|---|---|
| `hmz-bdm-morning-sweep/` | Morning job-search research and filtering |
| `hmz-bdm-evening-sweep/` | Evening job-search research and filtering |
| `hmz-daily-leads/` | Lead research and qualification |
| `hmz-indeed-mcp-sweep/` | Indeed-focused job-search procedure |

Read each `SKILL.md` before use. Requirements, data sources, filters, and expected outputs are defined there and may need revision for your location, eligibility, tools, and current platform rules.

## Status and limits

- The checked-in tree contains four skill folders; no runtime application or repository-wide installer is included in this snapshot.
- References to MCP connectors, web search, spreadsheets, or email describe workflow instructions. Their availability and execution are not verified here.
- A desired email or report output does not mean this repository sends one.
- No tests or live searches were run for this documentation update.

## Safe use

Treat job and lead research output as unverified until checked against the original source. Review search sources and eligibility filters before relying on them. Do not send messages, submit applications, or export personal data without a separate review of recipients, content, and destination.

Do not place API keys, account credentials, or private candidate/customer records in these files. Keep sensitive data in an approved local or secret-storage system.

See the [documentation index](docs/README.md).
