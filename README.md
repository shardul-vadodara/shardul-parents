# શાર્દૂલ શિશુ વિહાર — સાપ્તાહિક પ્રવૃત્તિ (Weekly Activity Portal)

Single-purpose static site for Shardul Shishu Vihar, Vadodara: weekly activity
access for parents and teachers, per age group. Hosted on GitHub Pages.

**Live:** https://shardul-vadodara.github.io/shardul-parents/

## What it shows

One feature — the week's plan, browsable by week (‹ › navigation, current week
auto-selected) and by group:

- **સાવજ-કેસરી** (૩.૫-૫.૫ વર્ષ) and **મૃગેન્દ્ર-પુંડરિક** (૫.૫-૮ વર્ષ)
- Per week: title, dates, main activities, ક્રિયાકલાપ (steps, materials,
  mahatva), parent note, festivals, season note
- Downloads: parent guide PDF / PNG per week (also useful for teachers)

## How content gets here

Content is authored in the private `active-parents` repo using the unified
planner tool (v4). The teacher clicks **પ્રકાશન પેકેજ સેવ કરો** which writes the
backup JSON + parent PDF/PNG into that repo's `exports/` folder, then commits
and pushes. A GitHub Action converts the data and pushes it here:

```
data/config.json   school info + groups
data/weeks.json    published weeks (generated — do not hand-edit)
files/             parent PDFs / PNGs (generated)
```

GitHub Pages redeploys automatically on every push (~1 minute).

## Constraints

- Static only (GitHub Pages free tier): no server, no login, no database
- This repo is public — never publish student names, phones, or photos
