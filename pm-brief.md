# PM Brief: Streakly Comeback Screen Prototype

## Target User

24-year-old who hit a 12-day streak, missed two days, and has not opened the app since. Matches Tom's profile from [interview-synthesis.md](02-research/interview-synthesis.md) — churned after breaking a 12-day streak in week 5.

## Job To Be Done

Get back in without feeling they lost everything.

## Feature

A personalized Comeback screen with three components:

- Best-streak stat
- One 60-second comeback lesson
- One-tap streak-freeze offer

## Constraint

Use data Streakly already has. No new integrations — matches Raj's confirmation in [decision-brief.md](decision-brief.md) that the concept is technically doable with existing data sources.

## Interview Decisions

These resolve the two items [decision-brief.md](decision-brief.md) explicitly flagged as unscoped (eligibility logic and freeze rules), plus prototype scope:

- **Trigger:** The Comeback screen appears every session after a break, persisting until the user acts on it or dismisses it — not a one-time interstitial.
- **Freeze mechanic:** Tapping the freeze retroactively restores the streak to its pre-break count (e.g. 12 → 12, not reset to 0).
- **Eligibility:** The freeze requires a minimum 7-day streak length and enforces a 90-day cooldown between freezes — a user who doesn't meet either condition sees an explanatory message instead of the freeze offer. (These limits were removed during an earlier review, then reinstated; see change_log.md for both decisions and their reasoning.)
- **Combinable actions:** Users can use the freeze *and* complete the comeback lesson in the same session — the lesson counts as today's activity, extending the restored streak by one (e.g. 12 → 13).
- **Scope:** Built as a short flow, not a single static screen — home (acknowledging the break) → Comeback screen → outcome (freeze confirmation / lesson complete / dismiss back to home).
- **Purpose:** This prototype is for a concept/usability test with real users, so it's built to feel real rather than internally annotated.
- **Tone:** Copy is specific to the user's own progress, avoiding guilt/failure language — directly responding to what Tom ("the app sent me this 'you lost your streak' notification that just made me feel bad") and NPS respondents flagged as the harshest part of today's experience.
