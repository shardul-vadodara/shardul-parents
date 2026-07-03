# શાર્દૂલ શિશુ વિહાર — માતાપિતા પોર્ટલ (Parent Portal)

Static parent-facing portal for Shardul Shishu Vihar, Vadodara. Hosted on GitHub Pages.

**Live:** https://shardul-vadodara.github.io/shardul-parents/

## What parents see

- **આ સપ્તાહ** — current week's plan per group (સાવજ-કેસરી / મૃગેન્દ્ર-પુંડરિક): summary, kriyakalapo, parent notes, festivals, downloads
- **ગૃહકાર્ય** — homework per group with due dates and attachments
- **પુસ્તકાલય** — library info and downloadable resources
- **સૂચનાઓ** — announcements (pinned ones stay on top)

## How to publish content

Everything is data-driven. Edit JSON files in `data/`, drop PDFs/PNGs into `files/`, commit, push. GitHub Pages redeploys automatically (~1 minute).

```
data/
  config.json         school info + groups (rarely changes)
  weeks.json          weekly plans (append a new week object each week)
  homework.json       homework entries
  library.json        library info + resource list
  announcements.json  announcements
files/                published PDFs / PNGs (referenced by path from JSON)
```

### Adding a week (`data/weeks.json`)

Append an object to the array. The site automatically shows the latest week whose `start_date` has arrived.

```json
{
  "week": 4,
  "start_date": "2026-07-06",
  "end_date": "2026-07-12",
  "title_gu": "સપ્તાહ ૪",
  "groups": {
    "savaj_kesari": {
      "summary_gu": "…",
      "kriyakalapo": [ { "title": "…", "steps": ["…"], "mahatva": "…" } ],
      "parent_note_gu": "…",
      "files": [ { "label_gu": "માર્ગદર્શિકા PDF", "path": "files/week4_sk.pdf" } ]
    },
    "mrigendra_pundarik": { "summary_gu": "…", "kriyakalapo": [], "parent_note_gu": "", "files": [] }
  },
  "festivals_gu": ["…"],
  "season_note_gu": "…"
}
```

The `kriyakalapo` format matches the JSON exported by the private weekly PDF generator tools (`title`, `steps[]`, `mahatva`), so exports can be pasted in directly.

### Homework (`data/homework.json`)

```json
{
  "id": "hw-2026-07-08",
  "date": "2026-07-08",
  "group": "savaj_kesari",        // or "mrigendra_pundarik" or "all"
  "title_gu": "…",
  "details_gu": "…",
  "due_date": "2026-07-12",
  "files": [ { "label_gu": "વર્કશીટ", "path": "files/hw_week4.pdf" } ]
}
```

### Announcements (`data/announcements.json`)

```json
{ "id": "ann-…", "date": "2026-07-08", "title_gu": "…", "details_gu": "…", "pinned": false }
```

### Library (`data/library.json`)

`info_gu` is the standing library note; `resources[]` entries with a non-empty `path` show a download button.

## Publishing from private repos

Content is authored in private repos (weekly planner tools). To publish:

1. Export parent PDF/PNG from the planner tool
2. Copy files into `files/`, update `data/weeks.json`
3. Commit and push to `main`

This can be automated later with a GitHub Action in the private repo that pushes to this repo using a fine-grained PAT.

## Constraints (GitHub Pages free tier)

- Static files only — no server, no database, no login
- Do not publish private/sensitive data (student names, phone numbers, photos with identifiable children) — this repo is public
- Site size limit 1 GB; keep PDFs lean
