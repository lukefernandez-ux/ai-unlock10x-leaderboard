# AI Unlock 10x Leaderboard

## What this is
A leaderboard dashboard for adtechnacity's AI enablement program ("AI Unlock 10x"). It tracks 28 participants across weekly exercises, awarding points for completion quality and speed.

## Architecture
- **`index.html`** — HTML skeleton + CSS + JavaScript rendering engine. No hardcoded data.
- **`data.json`** — Single source of truth for all participant scores, team rosters, and week metadata. ~5KB.
- **`avatars/`** — Participant robot photos and logo (`logo.png`). Named `firstname-lastname.jpg` (or `.png`).
- No build step. No dependencies. Static files served directly.

## data.json Schema
```json
{
  "teams": {
    "Team Name": {
      "color": "#hex",
      "cssClass": "team-tag-name",
      "short": "Short Label",
      "members": ["Full Name", ...]
    }
  },
  "weekMeta": {
    "week1": {
      "title": "Exercise Title",
      "task": "Description shown on leaderboard",
      "deadline": "Wednesday EOD",
      "maxPoints": 60,
      "latePolicy": "50% of base score, no speed bonus or BIC eligible"
    }
  },
  "participants": [
    {
      "name": "Full Name",
      "avatar": "avatars/first-last.jpg",
      "robot": "Robot Name",
      "weeks": {
        "week1": {
          "status": "full|partial|joined|none|ooo",
          "base": 40,
          "baseDesc": "Photo + 🤙",
          "speedTime": "20 min",
          "speedBonus": 10,
          "bic": 10,
          "bicDesc": "14 reactions",
          "late": false,
          "total": 60
        }
      },
      "ooo": true
    }
  ]
}
```

## Common Agent Tasks

### Update a participant's score
Edit `data.json` → find participant by name → modify their `weeks.weekN` object. The `total` field should equal `base + speedBonus + bic`. The rendering engine computes cumulative scores automatically.

### Add a new week
1. Add a `weekN` entry to `weekMeta` with title, task, deadline, maxPoints, latePolicy
2. Add a `weekN` object to each participant's `weeks` map
3. Tabs and views are generated automatically from `weekMeta` keys

### Add a new participant
Add an entry to the `participants` array with name, avatar (or null), robot (or null), and weeks data. Ensure the name appears in the appropriate team's `members` array.

### Update team rosters
Edit `teams` in `data.json`. Each team has `color`, `cssClass`, `short`, and `members`. A participant can be in multiple teams.

## Design
- **Font**: Geist
- **Primary accent**: Orange (#E8552D)
- **Background**: White
- **Text**: Black (#1a1a1a) headings, dark gray (#374151/#4b5563) body, medium gray (#6b7280) secondary

## Hosting
- **GitHub**: https://github.com/lukefernandez-ux/ai-unlock10x-leaderboard
- **Vercel**: https://ai-unlock10x-leaderboard.vercel.app (account: lukefernandez-1695)
- Deploy: `vercel --prod --yes`

## Views
- **All Weeks**: Cumulative standings across all exercises
- **Week N tabs**: Detailed view with task description, scoring breakdown, base/speed/BIC/total columns
- Week 1 is the default view

## Scoring System
- **Full completion** (all requirements met on first post): 40 pts base
- **Partial completion** (needed a reminder to fix post): 25 pts base
- **Joined only** (joined channel but didn't complete task): 10 pts
- **Has not started**: 0 pts
- **Speed bonuses**: Within 4h = +10 pts, within 12h = +5 pts, within 24h = +2 pts
- **Best in Class (BIC)**: +10 pts to top 5 participants by Slack reaction count. Week 1 max is now 60 pts.
  - Week 1 BIC recipients: Bao Tran (14 reactions), Rob Millie (12), Logan Dunn (9), Justin Marutz (9), Maya Golan (9)
- **Late submissions**: After the deadline, participants earn 50% of the base score only (no speed bonus or BIC eligible)

## Week 1 Task
Join #ai-unlock10x on Slack, post a photo of your favorite robot, and include a 🤙 emoji.
- **Deadline**: Wednesday EOD
- **Late policy**: 50% of base score (e.g. full late = 20 pts)
- Sumin Oh completed late (2026-03-12) — scored 20 pts

## Week 3 Task
Claude in Chrome — extend tool audit, identify 3 action workflows using Claude in Chrome, build one, record a screen capture.
- **Deadline**: Friday March 27, 12pm ET
- **Speed cutoff**: Thursday March 26, 12pm ET (speed bonus = +10)
- **Late policy**: 50% of base score, no speed/BIC eligible
- **No screen recording penalty**: -5 pts (applied to base)
- **BIC recipients (4)**: Sheba Lawrence, Sumin Oh, Nick Zollinger, Felipe Guarin
- **Not scored**: John Voigt (OOO), Christopher Silva (omitted), Michael Herrera (omitted this week)
- Cameron Thornton returned from OOO and submitted Week 3

## Data Sources
- **Slack channel**: #ai-unlock10x (C0ALKGTDYRW)
- **Avatar photos**: Cropped robot images from participant Slack posts, stored in `avatars/`
- **Participant list**: 28 people from adtechnacity

## Future Plans
- Add Week 2+ exercises with new tabs
- Auto-refresh from Slack API to pull completion data
- Google Drive integration for participant file uploads
- Hosted dashboard with live updates
