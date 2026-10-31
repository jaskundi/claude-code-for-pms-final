# 03 · Rewind — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly.

Last session you read four conversations and every support ticket
since 4.2 — and found the two piles did not agree.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.
Using the rook-database connector, analyse how responder acceptance, rejection, and missed ping rates changed after Release 4.2 on 12 August. Break down the results by week and identify whether the changes were driven by more rejections, more missed pings, or both. Show the actual counts, percentages, and underlying rows used in your calculations.

### 2.
Using the rook-database connector, investigate whether the changes after 12 August affected all responders equally or were concentrated among particular responders, locations, times of day, or other available segments. First inspect the pings table schema to identify which dimensions exist. Compare weekly counts and acceptance rates before and after the release for each relevant segment, and show the underlying rows supporting your findings.

### 3.
Using the rook-database connector, investigate whether the change in ping outcomes after 12 August is consistent with an impact from Release 4.2 or could be explained by other factors. Compare several weeks before and after the release, checking for pre-existing trends, changes in ping volume, responder mix, and any available confounding factors. Show the SQL queries, weekly results, and underlying rows. Clearly distinguish what the data proves, what it suggests, and what additional evidence would be needed to establish causation.

### 4.
If the Director of Product asked tomorrow what Release 4.2 actually did to responders, what's the one number you'd put in front of her?

### 5.
If I'd only asked for the number, not the rows, what would I have missed?
