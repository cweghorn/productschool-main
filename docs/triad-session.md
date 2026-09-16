# Streakly Comeback Screen — Triad Session

*Attendees: Christa (PM), Raj (Eng), Lena (Design). 30 minutes.*
*Grounding docs: [prototype/index.html](../prototype/index.html), [change_log.md](../change_log.md), [decision-brief.md](../decision-brief.md), [docs/hypothesis.md](hypothesis.md).*

## Agenda

**Goal:** Walk out with feasibility input from Raj, design input from Lena, and agreement on what happens next — not to re-litigate the problem (Marcus already signed off on that framing).

| Time | What |
|------|------|
| 0–5 min | Context: the Day-7 retention drop, Marcus's sign-off, why this prototype exists |
| 5–15 min | Live walkthrough of the prototype — both paths (freeze, lesson, combined) |
| 15–25 min | Open discussion — feasibility, unresolved design concerns, success metrics |
| 25–30 min | Recap decisions and owners |

### What to Show

- The live clickable prototype (`prototype/index.html`): the Comeback screen, the one-tap freeze button, the 60-second comeback lesson, and the combined outcome (13 days).
- The reasoning behind the current freeze interaction — a one-tap button rather than a toggle — from the persona playtest logged in `change_log.md` (Day 2).
- The hypothesis and the know/assume/don't-know breakdown in `docs/hypothesis.md`, to ground the discussion in what's evidence-backed versus still open.

### Questions to Ask Raj (Eng)

- Any feasibility or abuse/cost concern with an *unconditional* streak-freeze (no minimum streak length, no cooldown), or is the current scope fine to build as-is?
- What's a realistic build estimate once this scope is locked?
- What would we instrument to isolate Day-7 retention specifically among week-1 streak-breakers, and is there a guardrail metric worth tracking alongside it (e.g. signal that long-streak users aren't devaluing the mechanic)?

### Questions to Ask Lena (Design)

- Reaction to the persona playtest findings — any UX risk you'd flag that the playtest didn't surface?
- Two concerns are still open from the last playtest round: the screen's content is hardcoded to a 12-day example (doesn't scale to very new users), and there's no way to distinguish a restored streak from one that was never broken (Priya's "does this cheapen it" reaction). Worth solving now, or explicitly deferring?
- How would you want to structure the concept/usability test with real users that the decision brief calls for before we commit engineering time?

### Decisions to Walk Out With

1. **Feasibility + rough build estimate** for the freeze/lesson scope as currently prototyped. *(Owner: Raj)*
2. **Whether to address or explicitly defer** the two open design concerns (personalization gap, achievement-integrity distinction) before the next build pass. *(Owner: Lena + Christa)*
3. **Agreed primary metric + guardrail metric** for the eventual A/B test. *(Owner: Raj + Christa)*
4. **Next milestone and owner** — usability test date, or move straight to a scoped build.

---

## Post-Session Alignment Doc (Template)

*Fill in and save as its own doc after the session.*

# Triad Alignment — Streakly Comeback Screen

**Date:** ___
**Attendees:** ___

## What We Reviewed

- ___

## Feedback & Open Questions

| From | Feedback / Question | Resolved? |
|------|----------------------|-----------|
| Raj | ___ | ☐ |
| Lena | ___ | ☐ |

## Decisions Made

| Decision | Owner | Due |
|----------|-------|-----|
| ___ | ___ | ___ |

## Unresolved / Deferred

- ___

## Next Milestone

- ___
