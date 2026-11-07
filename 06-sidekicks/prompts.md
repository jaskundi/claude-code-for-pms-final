# 06 · Sidekicks — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. You've spent five sessions on it: finding out what
went wrong, then building the fix nobody had — a working prototype,
by hand, in one sitting, for one room.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.
Make a skill called review-checklist. When I point it at a brief, it checks that the brief: names who owns it, says how we'll know it worked, keeps the same scope start to finish, and explains the problem before the fix.

### 2.
Schedule review-checklist to run every Monday morning, and let me know what it finds. Nothing needs to be ready for it to fire today. I'm setting the habit, not waiting on the result.

### 3.
unsure if you need to run these checks?

```
review-checklist: scheduled run
Started: 2026-10-13 03:00 UTC
4 briefs checked, 4 flagged, 1 flag each.

bulk-callout.txt                  -> no owner named
routing-override-audit-log.txt    -> no success measure
requisition-approval-chains.txt   -> scope grows mid-document
handler-phone-app.txt             -> solution before problem
```
