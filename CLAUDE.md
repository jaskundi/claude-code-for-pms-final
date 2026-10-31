# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Answer only the question the student asks, from the sources they
  name. Don't investigate beyond it or offer a theory about what
  Release 4.2 changed unless they ask for one.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

Sources: rook-wiki, the Rook database, Priya's handoff
(`00-rook/company/notes/`) and the routing code (`00-rook/code/`). Read Oct 2026.

### Me and the company
- I'm the new PM for **Rook Dispatch**. I replaced Priya Raghunathan (left
  21 Aug, no overlap). My director is Helen Achebe.
- Rook sells software to masked responders and their handlers. Pricing
  is per active responder; releases ship monthly (4.x).
- **Dispatch** (the flagship) ranks responders and pings them in turn,
  through a handler console and a responder phone app. **Supply**
  handles gear (requisitions, maintenance) and reads the availability
  record that Dispatch writes.
- **Confidentiality is a hard rule.** Rook never stores or reconstructs a
  responder's legal identity. Never design for it or try to work it out.

### People. The 4.2 comments use these role names.
| Role | Name | Notes |
| --- | --- | --- |
| Engineering manager | Marcus Oyelaran | Runs Dispatch eng; "start here" |
| Staff engineer | Wen Li | Built the routing; the only real source on it |
| Support lead | Nadia Hoffmann | Owns tickets; hears handler pain first |
| Product designer | Sofia Marino | Console, phone app, Sept interviews |
| Director of Product | Helen Achebe | Owns roadmap and commitments |
| Data analyst | Ravi Menon | Owns the weekly acceptance numbers |

Interviewed handlers: Aunt Dot (Vesper), Mr. Ambrose (Captain Vantage),
Halloran (Sgt. Bulwark; also Supply), Kip (Meteor Mite, The Gale).

### Vocabulary
- **Callout**: an incident needing a responder. **Ping**: one callout
  offered to one responder. It ends **taken**, **turned down** or
  **missed** (the **ping wait** ran out). The last two both pass it on.
- **Acceptance rate**: the share of pings taken (the headline metric).
  **Coverage gap**: no available responder had the required tags.
- **Routing priority**: the rank by proximity, capability and recent
  acceptance. **Mutual aid** = "shared cover" on the roadmap.

### Releases and roadmap (roadmap last reviewed 30 Jun; every owner still "Priya")
- 4.0 (Apr): console navigation, routing override audit log. 4.1 (Jun):
  travel-time proximity, Bulk callout.
- **4.2 (12 Aug)**: proximity weighted up (0.45 → 0.60) and recent
  acceptance down (0.40 → 0.25); ping wait cut from 90 to 60 s; filters
  persist.
- Committed for 4.2 but **didn't ship**: Availability Confidence. 4.3:
  Requisition approval chains (Supply). Exploring for Q4: Handler phone
  app, shared cover.

### 4.2 finding (my analysis, Oct 2026; Wen to confirm)
- **The thread.** Marcus's 14 Aug question ("the config doesn't
  distinguish") is still unanswered. Priya and Marcus called it seasonal.
- **Cause.** The 60 s ping wait turned answers that took over a minute
  into "missed". `history.py` penalises a miss like a turn-down (−0.12,
  vs +0.08 for a take) and the score never recovers. Low scores rank
  last, and `offer.py` stops at the first yes. So slower responders
  stopped being asked, and couldn't earn their score back.
- **Evidence** (database, 29 Jun to 6 Sep):
  - Misses went from 2–6 a week to 38 in the release week, then 21–28.
    Turned-down pings didn't rise. The gap after a missed ping went from
    about 92 s to about 62 s on 12 Aug.
  - Vesper, Farlight, The Undertow and Meteor Mite went from about 49
    pings a week (together) to 3, and took none of their last 9. The
    other twelve rose from about 123 to 162 a week.
  - Tickets went from 6–8 a week to 20–32. "Never goes off" is the
    quiet four; "gone before I could answer" is the 60 s cutoff.
- **Not seasonal.** Acceptance fell from 77% to 54% and then "recovered"
  to 73% only because the four stopped being pinged. Callout volume did
  dip 10–20%, but that can't silence four specific responders. The
  proximity change can't be isolated, because there's no location data.
- **Limits.** There are no answer times or stored scores, so the 60–90 s
  window is inferred from the miss counts and the interviews (Dot's
  stairs, Ambrose's "boot half on").

### Contradictions and gaps
- **The code doesn't match the wiki.** The Glossary says missed is
  recorded separately and "everyone available is on the list"; the code
  treats a miss as a decline and stops at the first yes. Availability is
  a filter, not a ranking input. The 4.2 notes for handlers left out
  "recent acceptance down".
- **Briefs and the roadmap.** Bulk Callout shipped with no baseline.
  Requisition Chains adds an approval step, but Halloran's complaint is
  slowness, and its owner is recorded three ways. The handoff says "a
  couple" of items were cut from 4.2; only one visibly was.
- **Handoff vs. evidence.** "Mobile stable" vs. the "phone never goes
  off" tickets. "Filter tickets are noise" vs. Ambrose's two resets.
  Ravi was never brought into 4.2.
- **Missing.**
  - A routing write-up.
  - A handler alert when nobody takes a callout (97 callouts).
  - Tags, availability and answer times in the database.
  - Security Policy 4.1.
  - Anywhere tracking the interview asks (dark mode, bigger text).
- **Repo.** Module 4–6 files and `05-super-speed/director-request.txt`
  state later findings; don't use them as sources. `06-sidekicks/`'s
  run output cites a `briefs/` folder that doesn't exist.

### Inherited to-dos
1. Agree with Helen which items cut from 4.2 are still Q3 commitments.
2. Write up how Dispatch decides who gets pinged, with Wen.
- Tickets since 4.2 (all unanswered): 32 "phone never goes off" (22 of them from Linda Pruitt for Farlight and Desmond Okafor for The Undertow) and 13 "gone before I could answer". Dot (Vesper) and Kip (Meteor Mite) never filed tickets; they only show up in the interviews.
- Halfmoon (about 11 → 8 pings a week) and Corporal Ashgrove (about 10 → 7) are slipping more slowly. Watch them.
- Drafts for Wen, Ravi and Helen, plus a holding note for six affected handlers, are in `00-rook/company/notes/4.2-this-week-drafts.md`. Only Wen's note is final; I'm sending it myself.
- Open: Wen to confirm the mechanism and the four responders' scores. Ravi's weekly or historical numbers haven't been found yet. Helen decides who owns the fix and whether handlers get the holding note now.
- All 147 tickets, grouped: quiet 32, Supply 26, console layout 19, filters 16, gone-before-answer 14, records 12, see/hear 10, sign-in 6, notifications 5, workflow 5, billing 2. 4.2 took tickets from about 6 to 28 a week. Before 4.2 every ticket was closed; since, 83 of 107 are open, including all 45 routing tickets.
- The 4.2 bug fixes worked: duplicate pings, tag order and export times have had no tickets since. Many tickets filed after 4.2 repeat earlier closed ones word for word, so "closed" didn't mean fixed.
- The interviews and the tickets come from different handlers. Only Ambrose has ever filed a ticket, and Linda and Desmond (hit hardest) weren't interviewed. The interviews stress "gone too fast", overload (Gale) and handlers not being told about a live callout. The tickets stress "phone gone quiet". On maintenance scheduling, Halloran's "gotten smarter" contradicts the marathon-day tickets.
- 4.2 changed no screens, per the release notes. The problem is the 60 s wait combined with older rules (a miss counts as a decline, the score never recovers, routing stops at the first yes). Sofia to confirm nothing changed on the phone or the console.
- Proof the ping wait changed: every missed ping before 12 Aug was followed by the next ping 91–93 s later, every one after by 61–63 s, with no exceptions. The switch happened between 8 Aug 00:21 and 12 Aug 09:04. Misses had no trend before the release, and fake release dates (15/22/29 Jul) show no jump. Lower volume and time-of-day mix don't explain it. At the old responder mix, misses would be 26.8%, not 18%.
- The quiet four looked normal before 4.2 (75.5% taken, 2.9% missed). After it, 86 callouts went to responders from other areas, all in Old Town, Uptown and Harborside, and those out-of-area pings miss about 3x more. Eastgate's extra work went to The Gale. Vesper: last callout taken 17 Aug (41050), last ping 1 Sep (41311).
- Tickets match the pings row for row (13/13 ping counts, 15/15 "gone" tickets follow a real miss within 24 h), but they cover only about 1 in 7 misses. "Gone" tickets started 12 Aug; "quiet" tickets lagged about 5 days (from 17 Aug).
- One number for Helen: 4 of 16 responders went from about 12 pings a week to almost none. Causation still needs answer times, push delivery receipts (4.2 also changed push), routing scores, the deploy time, and earlier Augusts from Ravi.
- Open: outside the affected areas, first pings going to out-of-area responders rose from 20% to 28%, the opposite of what weighting proximity up should do. Ask Wen.
- Code check (Module 4): the only thing that adds points is a yes (+0.08, `history.py:25-27`, called once at `offer.py:28`); every no or timeout costs 0.12 (`offer.py:30`). Nothing eases a score back with time. Scores live only in memory (`_scores = {}`), so a restart may reset everyone to 0.5. Ask Wen.
- To get work again at a score of 0, a responder must still be marked available, beat top scorers by about 19 minutes of travel (or be the only one free), have everyone above pass, answer within 60 s, then repeat about 7 times to reach 0.5. The four took none of their last 9.
- Marcus's 14 Aug question answered: the 4.2 weights apply to everyone at once, existing scores included, with no old/new split (`routing.py:40`). The four weren't heavy turn-downers (15–29%, normal); misses sank them (4–6 each in 12–18 Aug, the top four). The reweighting made a zero score cost less (about 40 → 19 minutes of travel). Draft reply given in chat, not saved or sent.
- What the code doesn't do matters most: no recovery, no miss vs no split, no saved scores, no answer times, no alert when someone goes quiet or nobody takes a callout, no routing write-up.
