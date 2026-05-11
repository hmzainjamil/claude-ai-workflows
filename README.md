# claude-ai-workflows
Claude Code workflow patterns — orchestration, multi-agent, OODA loop, scheduled tasks

![Claude Code](https://img.shields.io/badge/Claude_Code-v2.1.89-orange?style=flat&labelColor=555) ![OODA](https://img.shields.io/badge/OODA_Loop-active-blue?style=flat&labelColor=555) ![L99](https://img.shields.io/badge/L99-Max_Performance-red?style=flat&labelColor=555)

Part of the [HMZ AI Infrastructure](https://github.com/hmzainjamil) stack.

---

## 🧠 CORE WORKFLOW PATTERNS

| Pattern | Trigger | Description |
|---------|---------|-------------|
| OODA Loop | Every prompt | Observe → Orient → Decide → Act — hardcoded behavioral mandate |
| L99 Mode | Always | Full capability, no hedging, no "it depends" stalling |
| Model Routing | Sub-tasks | Tier 0 (Ollama/Groq/Gemini) → Tier 1 (Haiku) → Tier 2 (Sonnet) |
| Skill Gating | UserPromptSubmit | Auto-activates relevant skills, deactivates after task |
| Memory | Stop hook | Auto-writes learnings to `~/.claude/session-queue.jsonl` |

## ⚙️ DEVELOPMENT WORKFLOWS

| Workflow | Pattern | Tools |
|----------|---------|-------|
| Agent Orchestration | Command → Agent → Skill | Paperclip API + scheduled tasks |
| Parallel Research | Multi-agent burst | Groq + Gemini + OpenRouter simultaneously |
| Code Generation | DeepSeek-V3 → review | OpenRouter → Claude final synthesis |
| PDF Reports | ReportLab direct | 11-page branded audit PDFs, no HTML intermediate |
| Audit Pipeline | Python scraper → PDF | Apify actors → ReportLab → email delivery |

## 💡 WORKFLOW RULES

■ **Model Routing Mandate (enforced on every task)**

```
TIER 0 (use first — zero Claude tokens):
  Ollama (local)     → general tasks, code
  DeepSeek-V3        → reasoning, complex analysis  
  Gemini 2.0 Flash   → research, drafting
  Groq (Llama 3)     → fastest cloud inference
  GPT-4o-mini        → standard tasks

TIER 1 (if Tier 0 unavailable):
  Claude Haiku 4.5   → smallest Claude, last resort

TIER 2 (final output only):
  Claude Sonnet 4.x  → conversation layer only
```

■ **Token Efficiency Rules**
- Never re-read files already read this session
- Never repeat information already in context  
- Batch all work into parallel calls
- Apply caveman compression to all sub-task outputs

---
Built by [HMZ](https://github.com/hmzainjamil) · [DigiMinds](https://digiminds.org)
