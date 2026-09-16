# Design Review — Streakly Comeback Screen

*Prepared for a design review with Lena (per [stakeholders/lena.md](../stakeholders/lena.md)), against [prototype/index.html](../prototype/index.html), [02-research/interview-synthesis.md](../02-research/interview-synthesis.md), and [docs/spec-readiness.md](spec-readiness.md). 2026-09-16.*

## What the Prototype Gets Right

- **Answers Tom's exact stated problem.** Tom: *"There was no way to recover it, nothing. So I gave up."* The one-tap streak-freeze is a direct answer to that.
- **Matches the mechanic Tom already said he wanted.** Per the interview synthesis, Tom explicitly said Duolingo's streak freeze "feels forgiving" — the prototype's one-tap restore matches that model.
- **Deliberately avoids the guilt tone Tom described** in the actual "you lost your streak" push ("made me feel bad") — the header copy is a direct rebuttal of that framing.
- **Echoes Priya's celebration instinct, partially.** Priya said what hooked her was "the app actually celebrating it... look what you built." The best-streak stat card leans on that same framing.

## Resolution — Updated After Follow-Up Review

### 1. Amara's day-4 experience — resolved

Early-tenure users on an **active** streak now get a genuinely distinct, independent celebration screen (see below) rather than a scaled-down version of Tom's break-recovery screen. This directly answers the blocking concern: Amara's fear ("I don't want to lose everything I've built after four days") is no longer met with a screen built around someone else's loss.

### 2. "Forgiving vs. guilt trip" — resolved, with a correction made in review

First draft copy proposed was *"Great job! You're on fire. Keep going!"* — flagged in review as exactly the pattern strategy.md warns against: *"not a generic 'keep going!' nudge."* Generic, not specific to the user's own progress, indistinguishable from any other streak app.

**Final copy, built into the prototype:** *"Day 4. Showing up 4 days in a row is the hardest part of building this — and you're already doing it."* Grounded in Priya's insight that habit formation takes roughly three weeks and "most people quit long before" — this names the early window as specifically hard, rather than a generic cheer.

### 3. Celebration moment placement — resolved

Confirmed and built as its own independent surface (`screen-celebration` in prototype/index.html) — shown for an active, unbroken streak, entirely unrelated to the Comeback/break-recovery flow. The prototype now includes a scenario switcher so both experiences (Tom's Comeback flow, Amara's Celebration screen) can be reviewed side by side.

### 4. Prototype/spec mismatch — resolved

Dismiss behavior confirmed: dismissing the screen returns it on the next session, consistent with docs/spec-readiness.md's "persists until acted on or dismissed" language.

---

## The Single Highest-Impact Change for Week-1 Retention

**Build a distinct, tenure-aware version of this experience for early-week-1 users (Amara's profile), instead of one template that scales numbers up or down.** *(Now built — see Resolution #1 and #3 above.)*

Why: the interview synthesis's own central finding is that week-1 users feel the streak's *risk* before they've banked any of its *reward* — the entire reason the Day-7 drop is concentrated in week-1 breakers. The original design was built around Tom (12 days, already had the reward, needs forgiveness) and generalized that same structure to Amara (4 days, still forming the habit, driven by anxiety, not loss). The independent celebration screen gives early-tenure users on an active streak a positive touchpoint that doesn't depend on failing first — directly addressing that mismatch instead of scaling the failure-recovery template down to a smaller number.

---

## Product Decision vs. Lena's Call

| Decision | Who owns it |
|----------|-------------|
| Whether the Comeback screen ships with a tenure-aware celebration variant for early-week-1 users, and whether it's in scope for this release | **Product decision** (Christa/Marcus) — resolved to "yes, build it" in this review, but the release-scope/timeline call is still Christa/Marcus's to make |
| The actual interaction/copy/visual design of that celebration screen (built as a first draft in this review) | **Lena** — the version in prototype/index.html is a first pass, not a final design signoff |
| Whether the celebration moment exists at all, and what business goal it serves | **Product decision** — resolved: yes, to give early-tenure users a non-failure touchpoint |
| Whether that celebration is its own independent surface vs. attached to the Comeback screen | **Product decision** — resolved: independent surface |
| Dismiss-and-returns-next-session behavior | Already resolved, consistent with the spec — no further decision needed |
| Final copy for the celebration screen ("Day 4. Showing up 4 days in a row...") | **Lena** — the current line is a first draft grounded in Priya's research quote, not a final signoff |
