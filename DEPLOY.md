# Glint Docs site

Static site from this markdown tree (no build step).

## GitHub Pages

1. Repo Settings → Pages → Source: **GitHub Actions**
2. Enable the workflow in [`.github/workflows/deploy-docs.yml`](.github/workflows/deploy-docs.yml)
3. Or: Pages → Deploy from a branch → `main` / `/` (root)

## Local preview

```bash
# from Glint-Docs
python3 -m http.server 8080
# open http://localhost:8080
```

## Index

Start at [README.md](README.md) → [Golden path](guides/golden-path.md) → [Smoke checklist](guides/smoke-checklist.md).
