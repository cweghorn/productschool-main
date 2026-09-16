# Streakly — Comeback Screen Prototype

A clickable HTML prototype of the Streakly Comeback experience, built for a concept/usability test with real users. Open [index.html](index.html) in a browser to try the flow.

## PM Brief

**Target User:** 24-year-old who hit a 12-day streak, missed two days, and has not opened the app since. Matches Tom's profile from [interview-synthesis.md](../02-research/interview-synthesis.md) — churned after breaking a 12-day streak in week 5.

**Job To Be Done:** Get back in without feeling they lost everything.

**Feature:** A personalized Comeback screen with three components:
- Best-streak stat
- One 60-second comeback lesson
- One-tap streak-freeze offer

**Constraint:** Use data Streakly already has. No new integrations.

## Key Decisions Made During the Interview

- **Trigger:** The Comeback screen appears every session after a break, persisting until the user acts on it or dismisses it — not a one-time interstitial. Dismissing returns to the home/acknowledgment screen; the offer reappears next session.
- **Freeze mechanic:** Tapping the freeze retroactively restores the streak to its pre-break count (e.g. 12 → 12, not reset to 0).
- **Eligibility: 7-day minimum, 90-day cooldown.** The freeze is only offered if the broken streak was 7+ days *and* the user hasn't used a freeze in the last 90 days. A user who doesn't meet both sees an explanatory message instead of the freeze button. *(These limits were removed in an earlier review, then reinstated — see change_log.md for both decisions.)*
- **Combinable actions:** Users can use the freeze *and* complete the comeback lesson in the same session — the lesson counts as today's activity, extending the restored streak by one (e.g. 12 → 13).
- **Scope:** Built as a short flow, not a single static screen — home (acknowledging the break) → Comeback screen → outcome (freeze confirmation / lesson complete / dismiss back to home).
- **Purpose:** Built for a concept/usability test with real users, so it's designed to feel real rather than internally annotated.
- **Tone:** Copy is specific to the user's own progress, avoiding guilt/failure language — directly responding to what Tom and NPS respondents flagged as the harshest part of today's experience.

## What's in the Prototype

- **Scenario switcher** — toggles between the Comeback flow (Tom's scenario) and an independent Celebration screen (Amara's scenario, an active day-4 streak, unrelated to any break).
- **Home screen** — acknowledges the broken streak explicitly instead of a blank reset; leads into the Comeback screen.
- **Comeback screen** — best-streak stat, comeback lesson, and a streak-freeze offer gated by the 7-day/90-day eligibility rule. A "preview" link lets you simulate the ineligible state (freeze used within 90 days) without waiting on real account data.
- **Celebration screen** — an independent surface for early-tenure users on an active streak, giving a positive touchpoint that doesn't require a break first.
- **Lesson flow** — a simulated 60-second lesson with a progress indicator.
- **Outcomes** — freeze confirmation (streak restored), lesson-complete state, and a "Not right now" path back to the acknowledged-break home screen.

See [pm-brief.md](../pm-brief.md) for the full brief and [docs/spec-readiness.md](../docs/spec-readiness.md) for the current requirements.
