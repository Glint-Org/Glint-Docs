# Copilot mode (AI + developer)

**Mode 3** of Glint’s [editor modes](../reference/editor-modes.md): you and an agent share the **Glint Web** frames board. The agent uses the same controls you do; you can watch, pause, edit, and teach.

> **Today:** In Glint Web, click **Allow agent** on the Copilot bar, then **Demo** to see a short live action. Mode 1 (manual) and Mode 2 (MCP / headless) remain the main ways to ship ZIPs. Deeper IDE attach is coming next.

## When to use Copilot

- You want to **see** the agent select frames, change scale/rotation, or swap bezels  
- You may **interrupt** mid-run (“stop - use this headline instead”)  
- You fixed one frame by hand and want: **“do the other frames like this”**  

Use **Headless / MCP** when you only need speed (CI, overnight packs).  
Use **Manual** when taste matters more than automation.

## How it works

```
You (chat or Demo)  →  Agent  →  Canvas actions  →  Live editor
                                 ↑                      │
                                 └── your edits ────────┘
```

- The open project (canvas + `.glint` / session) is the source of truth - not the chat  
- Visible moves map to the same actions as the sidebar (scale %, angle °, bezel, theme, …)  
- **Pause** stops the agent so you can edit safely  

## Try it

1. Open Glint Web with your frames loaded  
2. Click **Allow agent** on the Copilot bar  
3. Click **Demo** (or ask your coding agent once editor MCP tools are available)  
4. Watch the status line and frame highlight; hit **Pause** anytime  
5. After you fix one frame, ask the agent to match the others  
6. Export ZIP / Copy for Glint View as usual  

## Tips for agents

1. Prefer real screenshots - never invent UI tiles  
2. Re-read editor state after the human edits  
3. On **Pause**, stop until the user resumes  
4. Do not ask users for Capture LLM API keys  

## Teach-from-edit

| You do | Agent should |
|--------|----------------|
| Set Frame 1 device to 90% / −6° | Apply the same transform to other frames if asked |
| Change bezel on one slide | Propagate that bezel when asked to “match” |
| Edit one headline | Do not overwrite other copy unless asked |
| Extract theme once | Reuse that palette |

Say it clearly in chat: “use the **selected** device as the template.”

## Related

- [Editor modes](../reference/editor-modes.md)  
- [Using Glint](using-glint.md)  
- [AI workflow](ai-workflow.md)  
- [Architecture](../reference/architecture.md)  
- [Checklist](smoke-checklist.md)  
- [Glint-MCP](https://github.com/Glint-Org/Glint-MCP)  
