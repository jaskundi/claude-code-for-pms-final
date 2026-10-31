# 04 · X-Ray Vision — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session the numbers showed you what happened: a
ping used to wait ninety seconds and now it waits sixty, people
missed pings they used to catch, and missing one counts the same as
turning one down — so four responders stopped hearing from us
altogether.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.
What does this imply, are we able to confirm what went wrong in 4.2?

### 2.
Based on what you found, the reason some responders are getting no pings at all is? and because ?

### 3.
Using the rook-database connector, test whether the changes identified in Release 4.2 correspond with changes in responder acceptance, rejection, or missed ping rates after 12 August. Compare weekly results before and after the release, and identify which observed patterns support or contradict the hypothesis. Show the SQL queries, calculations, and underlying rows used as evidence.

### 4.
Find the engineering manager's unanswered question on the Release 4.2 wiki page. Investigate whether the relevant code changes and pings data can answer it. Identify the most likely root cause, distinguish confirmed evidence from assumptions, and show the code references and underlying database rows supporting your conclusion. Finally, draft a clear one-sentence answer I could give the engineering manager, including any important uncertainty.

### 5.
What would you tell a PM who's never opened a codebase about why this is worth doing as in the fix?

### 6.
If I'd only asked what the code does, not what it doesn't do, what would I have missed?

Also Marcus's question below:

Quick one, did the change to who gets asked first apply to responders who'd already been turning jobs down, or just new ones? Can't tell from the code and don't want to guess on this. Anyone know?

What would we reply with?

### 7.
If I'd only asked what the code does, not what it doesn't do, what would I have missed?
