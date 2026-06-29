# Longbridge Presence Monitor

Weekly health check for Longbridge's presence across MCP registries, skill directories, partner projects, and auto-generated homepage dashboard.

## What it does

- **Every Monday 02:00 UTC** — GitHub Actions runs three scripts:
  1. `check_registries.py` — checks all ✅ URLs in `tests/REGISTRY_CHECKLIST.md` and `tests/DISTRIBUTION_CHANNELS.md`, verifies each page still mentions Longbridge
  2. `check_sponsors.py` — checks ★★★ open-source projects and `tests/watch-sponsors.json` for Longbridge mentions in their READMEs
  3. `generate_homepage.py` — renders `docs/index.html` dashboard from latest reports
- Results are committed back to this repo automatically
- If any ❌ failures are detected, a GitHub Issue is opened automatically

## Structure

```
scripts/
  check_registries.py       # batch URL health check
  check_sponsors.py         # sponsor / partner project check
  generate_homepage.py      # homepage generator
tests/
  REGISTRY_CHECKLIST.md     # MCP registry submission list
  DISTRIBUTION_CHANNELS.md  # skill & CLI distribution channels
  awesome-finance-opensource.md  # finance OSS projects (★★★ auto-checked)
  watch-sponsors.json       # manually maintained sponsor list
  reports/                  # generated reports (committed weekly)
docs/
  index.html                # generated homepage dashboard
.github/workflows/
  registry-health-check.yml # weekly cron + issue creation
```

## Adding a sponsored project

Edit `tests/watch-sponsors.json`:

```json
{
  "sponsors": [
    {
      "name": "Project Name",
      "github_url": "https://github.com/org/repo",
      "repo": "org/repo",
      "notes": "Why we track this"
    }
  ]
}
```

## Manual run

```bash
pip install requests
python scripts/check_registries.py
python scripts/check_sponsors.py
python scripts/generate_homepage.py
```

## Reports

Latest reports: [`tests/reports/`](tests/reports/)  
Homepage: [`docs/index.html`](docs/index.html)
