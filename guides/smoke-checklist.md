# Checklist

Use this to confirm Glint works on your machine. Check each box as you go.

## Capture (Flutter)

- [ ] `glint init` in a Flutter app writes `glint.yaml` and a test stub  
- [ ] `glint capture` produces PNGs + `session.json` (try `pixel9` first)  
- [ ] `session.json` lists screens whose image paths open correctly  

## Bridge (Android / web)

- [ ] `python glint.py devices` lists your ADB targets  
- [ ] `python glint.py capture` writes a PNG and session  
- [ ] `python glint.py start` shows a pairing token on `ws://127.0.0.1:7700`  
- [ ] Glint Web can receive a frame from the Bridge  

## Web editor

- [ ] `npm run build` succeeds in Glint-Web  
- [ ] Import a Capture/Bridge folder - screenshots land on frames  
- [ ] Changing template keeps your screenshots  
- [ ] Export ZIP matches the store size you picked  
- [ ] **Copy for Glint View** pastes a session View can open  

## View

- [ ] Paste session - listing preview shows frames at store aspect  

## Agents (optional)

- [ ] MCP `glint_validate_session` accepts a Capture folder  
- [ ] MCP `glint_export` (or Web export) produces a ZIP  

Next: [Golden path](golden-path.md) · [Store upload](store-upload.md)
