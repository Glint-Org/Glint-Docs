# Editor modes (Manual · Headless · Copilot)

Glint uses the **same actions** everywhere - import shots, pick a template, set bezel, scale, rotate, theme, export. You choose how those actions run:

| Mode | Who drives | What you see | Best for |
|------|------------|--------------|----------|
| **1. Manual** | You in Glint Web | Full editor | Polish and last-mile taste |
| **2. Headless / MCP** | Agent or CI via tools | Final screenshots / ZIP | Speed and automation |
| **3. Copilot** | You + agent on one board | Agent actions live in the editor | Demos, trust, teach-by-edit |

```
                    ┌─────────────────────────┐
                    │   Same editor actions    │
                    │  select · scale · angle  │
                    │  bezel · theme · export  │
                    └────────────┬────────────┘
           ┌─────────────────────┼─────────────────────┐
           ▼                     ▼                     ▼
     ┌───────────┐        ┌─────────────┐       ┌──────────────┐
     │  Manual   │        │ Headless /  │       │   Copilot    │
     │  (UI)     │        │ MCP         │       │  UI + agent  │
     └───────────┘        └─────────────┘       └──────────────┘
```

## Mode 1 - Manual

Open Glint Web, import a session or PNGs, pick a template, edit frames (bezel, scale %, rotation °, colors, headlines), export ZIP, optionally hand off to View.

- No agent required  
- Work stays in the live canvas and `.glint` pack  
- Guide: [How to use Glint](../guides/using-glint.md) · [Workflow](../guides/workflow.md)  

## Mode 2 - Headless / MCP

An IDE agent (Cursor, Claude Code, Copilot) or CI calls **MCP / CLI** tools. Work happens offstage - you review the **outputs** (session folder, rendered PNGs, ZIP).

Typical tools: discover / capture / Bridge crawl / validate / render / export.  
Guide: [AI workflow](../guides/ai-workflow.md) · [Glint-MCP](https://github.com/Glint-Org/Glint-MCP)

**Rules:** prefer real app screens; never fabricate UI tiles; do not paste Capture LLM keys into the product for polish.

## Mode 3 - Copilot

You and an agent share the Glint Web board. The agent drives the same controls; you can watch, pause, and teach (“I fixed frame 1 - do the others like this”).

**In the editor today:** Copilot bar → **Allow agent** / **Pause** / **Demo**, with a live status line and frame highlight.

Guide: [Copilot mode](../guides/copilot-mode.md)

## Which mode should I use?

| Situation | Use |
|-----------|-----|
| Tweaking one headline by eye | **Manual** |
| CI or overnight store ZIP | **Headless / MCP** |
| Demo or “watch the AI work” | **Copilot** |
| Capture only, design later | Capture/Bridge → then any mode |

## Related

- [Copilot mode](../guides/copilot-mode.md)  
- [AI workflow](../guides/ai-workflow.md)  
- [Using Glint](../guides/using-glint.md)  
- [Architecture](architecture.md)  
