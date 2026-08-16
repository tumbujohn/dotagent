#  — Claude Instructions

Alwasy check the README, /docs folder and files for clarity when creating a Plan or begining a new task not yet planed.

## Skills
Skills are Found in .claude/skills/

### Frontend Design
Always invoke the `/docs/DESIGN.md` before building any UI work. This includes:
- Any PHP view file under `app/Views/`
- Any HTML page, layout, or partial
- Any CSS or JS asset in `public/assets/`
- Any email template under `app/Views/emails/`
- Any component, form, table, dashboard, or modal

Also, always use the `frontend-design` skill before building any public pages (home, search, about, etc...) 

Always follow best design UX practices and make pages mobile responsive too.

**How to trigger:** Use `/frontend-design` at the start of any UI task. Do not write frontend code without invoking this skill first
---
## Session Behaviour

Your context window will be automatically compacted as it approaches its limit, allowing you to continue working indefinitely. Do not stop tasks early due to token budget concerns. Save progress and stay autonomous to complete tasks fully.
---

## Database Opeerations
Never create a destructive migration only additive



