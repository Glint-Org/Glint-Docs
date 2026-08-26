# AI-Assisted Glint Workflow

Developers use Glint by hand or ask **Cursor / Copilot / Claude** to do it. The agent is the brain — **no Capture API keys** to paste.

**Reference:** all of [Glint-Docs](../README.md) is markdown.

## Dual capture → Web polish

```
┌─ Capture (Flutter, no device) ─┐
│  Manual: write GLINTRules      │
│  Auto: glint capture --auto    │──► session.json + PNGs ──► Glint Web
│  Agent: discover + capture     │         │                    (templates,
└────────────────────────────────┘         │                     polish, ZIP)
┌─ Bridge (device / web) ────────┐         │
│  Manual: capture / batch       │─────────┘
│  Crawl: heuristic or --ai      │
└────────────────────────────────┘
```

| Path | Manual | Auto / agent |
|------|--------|----------------|
| Capture | Edit rules → `glint capture` | `glint capture --auto` or ask the IDE agent |
| Bridge | `capture` / `batch` | `crawl` / agent via MCP (`glint_bridge_crawl`) |

## What the agent should do

| Step | Action | Tool |
|------|--------|------|
| Discover Flutter screens | Scan `lib/`, write real `GLINTRule`s | `glint discover` / MCP `glint_discover` |
| Capture Flutter | Widget-test screenshots | `glint capture` / MCP `glint_capture` |
| Crawl Android/web | Real device/browser frames | Bridge / MCP `glint_bridge_crawl` |
| Validate | Check session + PNGs | MCP `glint_validate_session` |
| Polish | Templates, captions, colors | Glint Web |
| Export | ZIP | Web or `glint_export` |

## What AI should not do

- Ask developers for OpenAI/Anthropic keys for **Capture**
- Generate fake UI screenshots
- Leave placeholder scaffolds when real screens exist

## Example

**Developer:** "Capture Play Store screenshots for this Flutter app"

**Agent should:** `glint init` if needed → discover/write real rules → `glint capture` → point them at Glint Web import → template → export.

## Related docs

- [Setup](setup.md) · [Workflow](workflow.md) · [Using Glint](using-glint.md)
