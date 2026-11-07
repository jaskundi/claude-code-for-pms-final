# Brief: No one goes quiet without anyone knowing

Draft for Helen · Dispatch PM · Nov 2026 · Not final: open questions at the bottom

## The problem, told through one responder

**Vesper** used to get about 12–14 pings a week and take most of them. Their
handler, **Aunt Dot**, says it takes a moment to get down the stairs to the
phone. Before 12 Aug that was fine, because a ping waited 90 seconds.

Release 4.2 cut the wait to 60 seconds. Vesper started missing pings, and
the routing scores a miss exactly like a "no". The score dropped with every
miss, and nothing ever lets it climb back on its own. Vesper took their last
callout on 17 Aug and got their last ping on 1 Sep. Since then the system
has quietly stopped asking.

**Nobody was told.** Not Vesper, not Dot, not support. Dot never filed a
ticket. We only know because she mentioned it in an interview. Three other
responders (Farlight, The Undertow, Meteor Mite) are in the same place, and
two more (Halfmoon, Corporal Ashgrove) are slipping.

**What went wrong isn't just the 60 seconds.** It's that the system can push
someone out with no warning, no reason given, and no way back.

## What we'd build

Three changes. The first two are things people see.

**1. A heads-up for the handler: "Vesper has gone quiet"**
- On Dot's console, Vesper's card shows a plain warning, for example *"Vesper
  hasn't been asked in 5 days (usually about 12 pings a week)."*
- A second warning goes on any responder who has missed 2 pings in a row:
  *"Vesper missed 2 pings: they timed out before an answer."*
- Each warning has one action: **"Send Vesper the next suitable callout."**
- *What Dot would notice:* she hears in days, not never, and can do
  something about it herself.

**2. A straight answer for the responder**
- When a ping times out, Vesper's phone says *"This one moved on after 60
  seconds. A timeout doesn't count against you."* It doesn't just disappear.
- *What Vesper would feel:* missed, not rejected. They aren't left
  wondering why the phone went silent.

**3. Fairer rules underneath** (the part engineering said is small)
- **A timeout is not a "no".** Only a real "no" lowers the score.
- **Scores recover.** A score slowly drifts back toward the starting point
  (0.5) over a few weeks. This is the question Wen's 2019 note asked.
- **A way back.** Someone who hasn't been asked in 5 days is offered the next
  callout they're suited for, even if they aren't top of the list.

## How we'd know it worked
- Vesper and the other three get back to roughly their old ping levels
  (about 12 a week each).
- Misses fall back toward the old 2–3% of pings. They're about 13–18% now.
- "Phone never goes off" tickets stop arriving. There have been 32 since 4.2,
  and none have been answered.
- No responder goes 5 days without a ping without their handler seeing a
  warning.

## Not doing
- **Quietly changing one number.** Putting the wait back to 90 s alone would
  repeat the mistake: the rules underneath would still push the next slow
  week's responders out, silently.
- **Showing handlers the raw score.** A warning they can act on beats a
  number they'd have to interpret.

## Open questions (needs an answer before build)

| # | Question | Who |
|---|---|---|
| 1 | Does the live system match the code? Are scores held only in memory, and do restarts reset them? What are Vesper's and the other three's scores right now? | Wen |
| 2 | Vesper is already at the bottom. Do we reset the four to 0.5, restore their 11 Aug scores, or let the new rules bring them back? | Helen, with Wen |
| 3 | Should the wait stay at 60 s? We have **no answer times**, so nobody knows how long real answers take. Can we start recording them? | Ravi, Wen |
| 4 | Are 5 days and 2 misses the right warning levels? | Sofia, with handlers |
| 5 | Wording and placement on the console and phone. | Sofia |
| 6 | Who owns this? The roadmap still lists Priya. | Helen |
| 7 | Baseline numbers before we ship. Bulk Callout shipped without one. | Ravi |

## Risks
- **The busiest responders lose some work.** The Gale and Nightwell picked
  up the slack. Their handlers need warning that their load will drop.
- **Supply reads the availability record.** If any of this touches it,
  Supply must be told first.
- **Confidentiality.** Warnings name responders by their responder name
  only. Nothing here stores or hints at who they are.
- **Being honest with handlers.** The 4.2 notes left out the ranking change.
  This release's notes should say plainly what changed and why.
