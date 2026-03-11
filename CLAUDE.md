# AI Unlock 10x Leaderboard

## What this is
A leaderboard dashboard for adtechnacity's AI enablement program ("AI Unlock 10x"). It tracks 28 participants across weekly exercises, awarding points for completion quality and speed.

## Architecture
This is currently a single static HTML file (`index.html`) with all data, styles, and avatar images embedded inline (base64). No build step required.

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
- **Week 1 (default)**: Detailed view with task description, scoring breakdown, base/speed/total columns

## Scoring System
- **Full completion** (all requirements met on first post): 40 pts base
- **Partial completion** (needed a reminder to fix post): 25 pts base
- **Joined only** (joined channel but didn't complete task): 10 pts
- **Has not started**: 0 pts
- **Speed bonuses**: Within 4h = +10 pts, within 12h = +5 pts, within 24h = +2 pts
- **Top 10% bonus**: TBD for future weeks

## Week 1 Task
Join #ai-unlock10x on Slack, post a photo of your favorite robot, and include a 🤙 emoji.

## Data Sources
- **Slack channel**: #ai-unlock10x (C0ALKGTDYRW)
- **Avatar photos**: Cropped robot images from participant Slack posts, embedded as base64
- **Participant list**: 28 people from adtechnacity

## Future Plans
- Add Week 2+ exercises with new tabs
- Auto-refresh from Slack API to pull completion data
- Google Drive integration for participant file uploads
- Hosted dashboard with live updates
