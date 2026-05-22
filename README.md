# Jesseman OS Dashboard

Static dashboard for the 75-day cut + 24-day Stratum Content sprint.

## What this is

A single-page dashboard rendered from `reference/dashboard/dash.py` in the parent workspace. Tracks:

- **Business sprint:** 3 retainers / 768 DMs / 48 sample rewrites by 2026-06-15
- **Body cut:** 87 → 70 kg by 2026-08-06 (milestone 77 kg by 2026-06-15)
- **Daily workout tab** — auto-switches by day of week (BB / CT / SA / REST)

## Stack

- Pure static HTML (no framework)
- Inline SVG sparklines
- HTML5 `<details>` for collapsible workout panel
- Vercel hosting (free tier, Git auto-deploy)

## How it stays in sync

1. Local: `/log-day` (Claude Code) → writes `reference/dashboard/data.json` + rebuilds HTML via `dash.py`
2. `dash.py` writes a copy of `index.html` here
3. Push to GitHub → Vercel auto-deploys
4. URL refreshes within ~30 seconds

## Privacy

- `X-Robots-Tag: noindex, nofollow` set globally
- URL is intentionally obscure (`jesseman-os-{hash}.vercel.app`)
- No auth — relies on URL obscurity. Don't share publicly.

## Local rebuild

```bash
cd /Users/jesseman/Downloads/Claude
python3 reference/dashboard/dash.py build
# (dash.py copies output to projects/jesseman-os/index.html)
cd projects/jesseman-os
git add -A && git commit -m "log $(date +%Y-%m-%d)" && git push
```

Vercel deploys automatically on push.
