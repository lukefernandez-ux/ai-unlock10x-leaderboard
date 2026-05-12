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
- **Best in Class (BIC)**: +10 pts. Recipients are assigned by Luke each week — not computed from reactions or any other signal. Week 1 max is now 60 pts.
  - Week 1 BIC recipients: Bao Tran, Rob Millie, Logan Dunn, Justin Marutz, Maya Golan
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

## Week 6 Task
Personal Software — build something in Claude Code you'd actually use every week, with CLAUDE.md + plan mode. Post walkthrough, CLAUDE.md, 3-min screen recording, reflection.
- **Deadline**: Wednesday April 29, 5pm ET
- **Speed cutoff**: Tuesday April 28, 5pm ET (speed bonus = +10)
- **Late policy**: -10 pts, no speed/BIC eligible
- **BIC recipients (5)**: Jonathan Choi, Rob Millie, Erik Orr, Cameron Thornton, Ruben Llibre
- **Late submissions**: Diana Oh (~33 min late, -10), Jimmy Gutowski (~21 hr late, -10)
- **Deductions**: Vartan Davidian -5 (no CLAUDE.md → 45), Will Oviedo -5 (no CLAUDE.md → 35), Melisa Singh -5 (no screen recording → 35)
- **Not scored**: Sheba Lawrence (OOO), Keri Flynn (no submission), Christopher Silva (omitted), Michael Herrera (omitted)
- **Removed from program**: Felipe Guarin (effective Week 6, will not be scored going forward)

## Week 7 Task
From v1 to v2 — use four lenses (Self, User, Code, Market) to find what to improve in your Week 6 build, capture insights with a custom `/idea` slash command (saved to `IDEAS.md`), then ship 3+ improvements. Submit a screenshot of insights + shipment descriptions.
- **Deadline**: Friday May 8, 3pm ET
- **Speed cutoff**: Thursday May 7, 3pm ET (speed bonus = +10)
- **Late policy**: -10 pts, no speed/BIC eligible (overridden by Luke for select Week 7 recipients)
- New skill introduced: custom Claude Code slash commands (`.claude/commands/<name>.md`). The lesson walks each participant through building `/idea` as their first one.
- **BIC recipients (5)**: Bao Tran, Jimmy Gutowski, Sumin Oh, Sheba Lawrence, Lisa Frendahl (Bao and Sumin were late — Luke override)
- **Late submissions**: Bao Tran (~59 min, -10), John Voigt (~1h 44m, -10), Nick Zollinger (~47 min, -10), Sumin Oh (~3h 43m, -10)
- **Common deduction**: -5 for shipments not lens-tagged (insight-to-shipment attribution missing). Applied to: Justin Marutz, Melisa Singh, Caroline Moore, Erik Orr, Rob Millie, Tom Raczkowski, Cameron Thornton, Lisa Frendahl, Sumin Oh
- **Other deductions**: Ruben Llibre -10 (no insights/lens documentation in post — only shipped fixes)
- **Not scored**: Keri Flynn (no submission), Vartan Davidian (no submission), Christopher Silva (omitted), Michael Herrera (omitted), Felipe Guarin (removed from program)

## Week 5 Task
The Power of Memory — create a Claude Project with system prompt + uploaded file, share the system prompt and a screenshot, and write thoughts on the "perfect project brain."
- **Deadline**: Friday April 17, 3pm ET
- **Speed cutoff**: Thursday April 16, 5pm ET (speed bonus = +10)
- **Late policy**: -10 pts, no speed/BIC eligible
- **BIC recipients (5)**: Ruben Llibre, Will Oviedo, Jimmy Gutowski, Cameron Thornton, Sheba Lawrence
- **Late submission**: Ryan Johnston (~38 min late, -10)
- **Deductions**: Sumin Oh -5 (no screenshot → 35), Keri Flynn -10 (no system prompt, no perfect brain section → 30)
- Bao Tran submitted 21 seconds after 3pm ET — graced to on-time
- **Not scored**: Vartan Davidian (no post), Christopher Silva (omitted), Michael Herrera (omitted)

## Week 8 Task (FINAL)
Where AI Fits, Where It Doesn't — final reflection that translates 7 weeks of individual builds into organizational sensemaking. Six sections: red/yellow/green inventory of what they built per week, where leverage actually is, infrastructure/tooling gaps (for product/eng), tiered blockers (for execs), strategy questions (for the CEO), three honest takes.
- **Deadline**: Friday May 15, 5pm ET
- **No speed bonus this week** — this is reflection, not a race
- **Scoring**: 40 base + 10 BIC = 50 max. Late = -10, no BIC eligible
- **Audience**: Luke + each participant's manager + Chris (CEO). Stated explicitly in the brief opening.
- **Design principle**: success = sharpest insight about where AI fits and doesn't, not who built the most. Red is the high-status answer.
- **Standardized submission format**: `week8-template.md` — fixed H2 headers, 🟢/🟡/🔴 tags, bulleted answers with `___` placeholders. Participants save as `firstname-lastname.md` and drop in Luke's Drive folder. Same structure must work for manager skim + Claude aggregation.
- **Private calibration**: `week8-prereads.md` — Luke's per-person behavioral read across weeks 1–7. Not shared. Used to spot self-assessment gaps when reading the briefs.
- **Synthesis tooling**: deferred — Luke will decide after seeing what submissions look like.

## Data Sources
- **Slack channel**: #ai-unlock10x (C0ALKGTDYRW)
- **Avatar photos**: Cropped robot images from participant Slack posts, stored in `avatars/`
- **Participant list**: 28 people from adtechnacity

## Future Plans
- Add Week 2+ exercises with new tabs
- Auto-refresh from Slack API to pull completion data
- Google Drive integration for participant file uploads
- Hosted dashboard with live updates
