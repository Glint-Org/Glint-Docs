# Glint Docs site

Markdown in this repo is the source of truth. Developers can:

1. **Read in GitHub** - browse `.md` files in the repo
2. **Read as a website** - Docsify on GitHub Pages (same files)

**Site URL:** https://glint-org.github.io/Glint-Docs/

## Enable GitHub Pages (one-time)

Your Actions workflow (`deploy-docs.yml`) only works if the Pages **Source** is **GitHub Actions**.

### If you see "Source: Branch" (current mistake)

That mode builds from `main` with GitHub's default Pages job. It can make the site live, but **`actions/deploy-pages` will fail with 404** ("Failed to create deployment").

Fix:

1. Open https://github.com/Glint-Org/Glint-Docs/settings/pages  
2. Under **Build and deployment → Source**, open the dropdown  
3. Choose **GitHub Actions** (not "Deploy from a branch")  
4. Save if prompted  
5. Open **Actions** → **Deploy Glint Docs** → **Run workflow** → wait for green  

You should see the environment `github-pages` update from that workflow.

### First-time setup

1. Same Pages settings URL  
2. Source → **GitHub Actions**  
3. Push to `main` or run the workflow manually  

Do **not** use GitHub Enterprise private Pages. Public free Pages is enough.

## Local preview

```bash
cd Glint-Docs
python3 -m http.server 8080
# open http://localhost:8080
```

## Link from other projects

| Doc | Pages URL |
|-----|-----------|
| Home | https://glint-org.github.io/Glint-Docs/ |
| Golden path | https://glint-org.github.io/Glint-Docs/#/guides/golden-path |
| Editor modes | https://glint-org.github.io/Glint-Docs/#/reference/editor-modes |
| Copilot | https://glint-org.github.io/Glint-Docs/#/guides/copilot-mode |
| AI workflow | https://glint-org.github.io/Glint-Docs/#/guides/ai-workflow |

Repo (raw markdown):

`https://github.com/Glint-Org/Glint-Docs/blob/main/guides/golden-path.md`

## Index

Start at [README.md](README.md) → [Golden path](guides/golden-path.md) → [Smoke checklist](guides/smoke-checklist.md).
