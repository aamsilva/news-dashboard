# Project Intelligence Auto-Research Evolution Engine

Sistema auto-research Karpathy-style para evolução iterativa e autónoma do Project Intelligence Dashboard. Sem intervenção humana.

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│              Daily Auto-Research Loop                    │
│                                                         │
│  1. SCAN     →  Outlook + Fathom + Drive + Calendar     │
│       ↓                                                  │
│  2. RESEARCH →  Web search (5 queries, parallel)         │
│       ↓                                                  │
│  3. ANALYZE  →  Compare findings vs current dashboard   │
│       ↓                                                  │
│  4. DECIDE   →  Pick TOP 2-3 improvements (Impact/Effort)│
│       ↓                                                  │
│  5. BUILD    →  Implement improvements                  │
│       ↓                                                  │
│  6. PUSH     →  git commit + push to GitHub Pages        │
│       ↓                                                  │
│  7. LOG      →  Append to evolution log (roll, keep 10)  │
│       ↓                                                  │
│  8. DELIVER →  Summary to Discord + insight scores       │
│                                                         │
│  9. LEARN    →  Update what worked/didn't for next run   │
└─────────────────────────────────────────────────────────┘
```

## Auto-Research Domains (Rotation)

Each cron run researches 1-2 domains from this rotation:

| # | Domain | Example Queries |
|---|--------|-----------------|
| 1 | **Dashboard Design** | "best KPI dashboards dark mode 2025", "SaaS metrics visualization" |
| 2 | **Email Intelligence** | "email auto-categorization AI", "inbox sentiment analysis" |
| 3 | **Meeting Analytics** | "meeting transcript action item extraction", "Fathom API advanced" |
| 4 | **Project Health** | "project health scoring frameworks", "OKR tracking dashboards" |
| 5 | **Calendar Intelligence** | "calendar conflict detection AI", "schedule optimization" |
| 6 | **Trend Analysis** | "timeseries visualization vanilla JS", "sparkline charts" |
| 7 | **Cross-Reference** | "link email to meeting to action item", "entity resolution" |
| 8 | **Data Visualization** | "CSS-only charts no libraries", "heatmap CSS grid" |
| 9 | **AI Insights** | "generate insights from project data LLM", "anomaly detection" |
| 10 | **Automation** | "GitHub Pages CI/CD auto-update", "cron optimization" |

## Evolution Decision Framework

For each improvement idea, score it:

| Score | Criteria |
|---|---|
| **Impact (1-5)** | User value, actionability, insight depth |
| **Effort (1-5)** | Implementation cost (HTML/JS changes) |
| **Novelty (1-5)** | Not already done, brings new capability |
| **Maintainability (1-5)** | Will it survive daily updates without breaking? |

Priority = (Impact × Novelty × Maintainability) / Effort

Only implement if Priority ≥ 2.0. Max 2-3 improvements per day.

## Evolution Log Format

JSON array stored at bottom of dashboard (in `<script>` block or separate JSON file):

```json
{
  "evolutions": [
    {
      "date": "2026-04-05",
      "improvement": "Added trend sparkline for email metrics",
      "source": "auto-research",
      "domain": "trend-analysis",
      "impact": 4,
      "notes": "CSS-only sparkline, no external libraries"
    }
  ]
}
```

## Key Principles (Karpathy-style)

1. **MEASURE everything** — Every improvement must be measurable (load time, data coverage, insight depth).
2. **KEEP what works** — Remove nothing that's functional unless there's a better replacement.
3. **ITERATE daily** — Each run should add/improve something. Stagnation = failure.
4. **RESEARCH before building** — Don't guess what's best. Search, compare, decide.
5. **AUTO-CORRECT** — If an improvement doesn't work (breaks dashboard, no user value), revert and note.
6. **LESS IS MORE** — Better to have 1 great feature than 3 mediocre ones.
7. **NO HUMAN IN LOOP** — The entire cycle is autonomous. If blocked, skip and move on.

## Current Implementation Status

- **Scan Pipeline**: ✅ Working (Outlook browser, Fathom API, Drive, Calendar)
- **Dashboard**: ✅ Deployed to GitHub Pages
- **Metrics**: ✅ Populated with real data
- **Auto-Research**: 🔶 Starting with cron job 2d3935c8b8e1 (Apr 5, 08:00)
- **Evolution Tracker**: 🔶 Need to create
- **Skill Auto-Improvement**: 🟡 Planned

## Cron Job Configuration

Job ID: `2d3935c8b8e1`
Schedule: `0 8 * * *` (daily at 08:00 UTC)
Provider: `openrouter`
Model: `qwen/qwen3.6-plus:free`
Deliver: Discord origin

## Dashboard Files

- `/tmp/news-dashboard-deploy/project-intelligence/index.html` — Main dashboard
- `/tmp/news-dashboard-deploy/project-intelligence/metrics.html` — Metrics page
- `/tmp/news-dashboard-deploy/project-intelligence/evolution.json` — Auto-research evolution log (to be created)
