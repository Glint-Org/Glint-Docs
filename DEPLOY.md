# Glint Docs site

Markdown in this repo is the source of truth. Developers can:

1. **Read in GitHub** - browse `.md` files in the repo
2. **Read as a website** - Docsify on GitHub Pages (same files)

**Site URL:** https://glint-org.github.io/Glint-Docs/

## Enable GitHub Pages (one-time)

1. Open [Glint-Docs → Settings → Pages](https://github.com/Glint-Org/Glint-Docs/settings/pages)
2. Under **Build and deployment → Source**, choose **GitHub Actions**
3. Push to `main` (or run **Actions → Deploy Glint Docs → Run workflow**)
4. Wait for the workflow to finish - the site URL appears on the Pages settings page

Do **not** pick "Deploy from a branch" if you use the Actions workflow - Source must be **GitHub Actions**.

Visibility stays **public** (free). GitHub Enterprise private Pages is not needed.

## Local preview

```bash
cd Glint-Docs
python3 -m http.server 8080
# open http://localhost:8080
```

## Link from other projects

Use stable Pages paths, for example:

| Doc | Pages URL |
|-----|-----------|
| Home | https://glint-org.github.io/Glint-Docs/ |
| Golden path | https://glint-org.github.io/Glint-Docs/#/guides/golden-path |
| Editor modes | https://glint-org.github.io/Glint-Docs/#/reference/editor-modes |
| Copilot | https://glint-org.github.io/Glint-Docs/#/guides/copilot-mode |
| AI workflow | https://glint-org.github.io/Glint-Docs/#/guides/ai-workflow |

Repo (raw markdown) links still work:

`https://github.com/Glint-Org/Glint-Docs/blob/main/guides/golden-path.md`

## Index

Start at [README.md](README.md) → [Golden path](guides/golden-path.md) → [Smoke checklist](guides/smoke-checklist.md).
