# How to publish this profile README

This folder becomes the special repo **`Pranav0494/Pranav0494`** — GitHub shows its README on your profile page. Nothing is live until you push.

## 1. Push it live

```bash
cd "C:\Users\prana\OneDrive\Desktop\COLLEGE PROJECTS\Pranav0494"
git init -b main
git add -A
git commit -m "Add profile README"
gh repo create Pranav0494/Pranav0494 --public --source=. --push
```

The repo **must be public** and named exactly like your username, or GitHub won't show it on your profile.

## 2. Make the snake animation work (one-time)

The snake needs its GitHub Action to run once before the image exists:

1. On GitHub: repo **Settings → Actions → General → Workflow permissions → "Read and write permissions"** → Save.
2. Run it once: `gh workflow run snake.yml` (or Actions tab → "generate snake" → Run workflow).
3. Wait ~1 minute. It creates an `output` branch with the SVGs; after that it refreshes daily at midnight.

Until this runs, the snake section shows a broken image — that's expected.

## 3. Make your stats look alive (important!)

Right now **9 of your 10 repos are private**, which makes the public stats cards look empty:

- **Profile page → "Contribution settings" → check "Private contributions"** — so your contribution graph (and the snake) shows all your activity.
- The **Top Languages card only sees public repos** — currently that's just `Stock_Project`. Make your best repos public (`gh repo edit Pranav0494/KV_PUBLIC_SCHOOL --visibility public` etc.) and add one-line descriptions to each.
- Pin 4–6 repos on your profile (Customize your pins) — pins appear right below the README.

## 4. Dropping the cybersecurity angle (your pending decision)

Search `README.md` for `SECURITY BLOCK` — there are **2 marked blocks** (a bullet in whoami, and the Burp Suite badge in skills). Delete everything between the ▼▼ and ▲▲ comment markers.

The **AI-Augmented Vulnerability Detection** project card is NOT inside markers — you picked it as a featured project, and it's framed ML-first (XGBoost pipeline). If you want it gone too, delete its `<td>...</td>` block in the projects table and the table will collapse to one card.

## 5. Known quirks (found during research, all normal)

- **Trophy widget** (inside the "More stats" collapsible) currently returns HTTP 402 — its free public server is over quota. It comes and goes; it's hidden in the collapsible so a broken image never shows front-and-center. Delete it if you don't like the gamble.
- **Stats cards** run on `github-stats-extended.vercel.app` (the maintained successor of the deprecated `github-readme-stats`). Public instance = occasional slow loads. If cards ever break for long, self-hosting on free Vercel takes ~10 min.
- **GitHub caches images ~hours** (camo proxy). Edits to card URLs can take a while to show; add a dummy query param like `&v=2` to force refresh.
- **Scheduled Actions auto-disable after 60 days without repo activity** — if the snake freezes months from now, just re-enable the workflow in the Actions tab.

## Keeping the stats badges accurate (optional 2-minute step)

The `$ htop --stats` badges read from `stats.json`, refreshed daily by `.github/workflows/stats.yml`. Without a token, the workflow can only auto-refresh the contributions number; the PR/commit/issue numbers stay at their seeded values. To keep ALL numbers auto-updating (including private-repo PRs):

1. Create a token at https://github.com/settings/tokens → "Generate new token (classic)" → scope: `repo` → no expiration or 1 year.
2. In your own terminal (NOT in a chat): `gh secret set STATS_PAT -R PRANAV0494/Pranav0494` and paste the token when prompted.
3. Done — the workflow detects the secret automatically on its next run.

## What's in here

| File | Purpose |
|---|---|
| `README.md` | The profile page — animated header, typing intro, terminal blocks, skills, project cards, live stats, snake |
| `.github/workflows/snake.yml` | Daily GitHub Action that generates the contribution-eating snake (matrix-green) |
| `SETUP.md` | This file — delete before/after pushing if you want (it's harmless to keep) |
