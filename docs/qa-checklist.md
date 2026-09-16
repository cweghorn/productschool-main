# QA Checklist — Streakly Comeback & Celebration Screens

*Against [docs/spec-readiness.md](spec-readiness.md), [prototype/README.md](../prototype/README.md), and [prototype/index.html](../prototype/index.html). Originally written 2026-09-16; updated the same day after the home screen and 7-day/90-day freeze eligibility limits were reinstated (see change_log.md, Day 6).*

## 1. Edge Case List

### Empty states

- User has never held a streak at all (day-1/day-2 signup, zero history). Per spec-readiness.md this is explicitly **out of scope** for this flow — but nothing in the prototype demonstrates what these users see *instead*.
- "Best streak" is 0 or null (a direct consequence of the above, or a data-integrity gap). The stat card has no fallback state — it always renders a hardcoded number.
- No lessons available in the user's track (track completed, or deprecated/removed). The comeback lesson assumes a lesson always exists to serve.
- Celebration screen at very low day counts (Day 1 or Day 2) — "showing up 1 day in a row" reads awkwardly; the copy template needs to handle singular/plural and very-early values, not just "Day 4."

### Edge data conditions

- Streak of 1 broken (lowest possible break). With the 7-day minimum now reinstated, this is **ineligible** for the freeze — correctly shows the "unavailable" message in the prototype. Worth checking the message itself doesn't feel disproportionate or confusing for someone this early.
- User breaks their streak twice within a week (freeze used once, then breaks again shortly after). With the 90-day cooldown now reinstated, they are **not** eligible again on the second break — the prototype's eligibility-preview toggle demonstrates this state, but it's undefined whether "best streak" reflects their all-time max or just the most recent pre-break count.
- Boundary case: streak of exactly 7 days. Code reads `previousBest >= 7`, so exactly 7 is eligible — worth a real test to confirm the actual backend implements the same inclusive boundary.
- Boundary case: a freeze used exactly 90 days ago. The prototype's cooldown toggle is a binary demo flag, not a real day-count — this exact boundary is **not determinable** from the prototype and needs real date-math testing against the backend.
- Streak-freeze already used on a prior break, within the cooldown window. Now correctly blocks a new freeze per the reinstated rule — but there's still no defined rule preventing double-freezing the *same* break twice within one session (client-side guard exists; real backend enforcement is unverified).
- Very large streak counts (e.g. 400+ days) — untested for layout/number formatting.
- Corrupted or missing streak data from the backend (null/undefined instead of a number) — no fallback handling exists anywhere in this artifact.

### Timing scenarios

- Missed one day vs. missed many (e.g., gone for months). There is still no restore-window cutoff (unchanged by the Day 6 reversal), so both cases remain eligible for the *trigger* — but the copy is identical regardless of gap length, and eligibility for the *freeze itself* now also depends on the separate 7-day/90-day rule, not just how long they've been gone. Worth confirming the interaction between "how long since the break" and "does the freeze rule apply" is intentional.
- Time zone boundaries — "missed one day" depends on a day boundary that a traveling user could cross unexpectedly, causing a false break or a missed one. Not addressed anywhere in spec or prototype.
- Comeback shown "too late" — if a user ignores the Comeback screen for a long time and organically starts a fresh streak through some other path, is there a defined precedence rule for which screen (Comeback vs. Celebration) takes priority? Not addressed.
- Standard calendar edge cases (DST transitions, leap day) affecting day-boundary calculations.

### Permission states

- Notifications off. The Comeback screen's trigger relies on the user opening the app; if push is off, there's no path back in except an organic, unprompted reopen. This is a bigger deal here than in most features, since the original problem (Tom's story) was partly caused by a notification itself.
- Notification permission never granted (not just toggled off).
- Background app refresh off — could mean the client shows a stale streak/eligibility state on open. Not testable in a static HTML prototype; flagged for the real client implementation.

---

## 2. PM QA Pass — Screen by Screen

| # | Check | Result | Notes |
|---|-------|--------|-------|
| 1 | Best-streak stat renders clearly on the Comeback screen | **Pass** | Static, but renders correctly (🏆 12 days) |
| 2 | Tapping "Use streak freeze" restores the streak and confirms it | **Pass** | `useFreeze()` sets state, swaps button to a confirmation pill, shows a toast |
| 3 | Freeze cannot be double-triggered | **Pass** | Guarded in state (`if (state.freezeOn ...) return`) *and* the button is replaced by a non-interactive element after first use |
| 4 | Completing the lesson correctly extends the streak count in every state combination | **Pass** | Verified: freeze-then-lesson and lesson-only both resolve to consistent counts via `currentStreak()` |
| 5 | Freeze correctly disables and relabels "Not needed" once the lesson alone continues the streak | **Pass** | Matches the documented business rule exactly |
| 6 | Zero-streak-history users are excluded from this flow, per spec | **Cannot be determined** | No code path exists either demonstrating or violating this — the prototype has no concept of a user without a streak at all. **Blocking for launch**: the exclusion needs to be verified against real eligibility logic, not a static mock. |
| 7 | Celebration screen behaves as an independent surface, unrelated to any break | **Pass** | Reachable via the scenario switcher regardless of Comeback state; correct in intent. Hardcoded to a single "Day 4" value — fine for this review, but must be parameterized in the real build. |
| 8 | Dismissing the Comeback screen returns to the home screen, which leads back into it next time | **Pass** *(updated — was Fail)* | The home screen and "Not right now" dismiss control were added back in Day 6. Caveat: a single-page mock can't truly simulate a "next session" boundary, so the round-trip navigation is verified, but not literal cross-session persistence. |
| 9 | Copy is free of guilt/failure language across all screens | **Pass** | Comeback, lesson, and celebration copy all avoid blame framing |
| 10 | Completed/disabled states are accessible (keyboard focus, screen reader) | **Fail** | Completed/restored states are still rendered as plain `<div>`s (via innerHTML/outerHTML swaps), which drop button semantics and any ARIA labeling. Not blocking for *this* click-through prototype, but must not carry into the real implementation. |
| 11 | Freeze eligibility (7-day minimum, 90-day cooldown) correctly gates the offer in both directions | **Pass** | `freezeEligible()` correctly shows the active button when eligible and an explanatory message when not; verified via the built-in eligibility-preview toggle. Note: the toggle is a binary demo flag, not real date math — exact boundary behavior (e.g. "used 90 days ago to the day") is untestable here. |

**Blocking before launch:** #6 (zero-history exclusion unverifiable).
**Ship as known issues, fix before/at real build:** #7 (hardcoded single value), #10 (accessibility regression in the mock's completed-state pattern), #11's boundary-date behavior (needs real backend testing, not just the demo toggle).
**Resolved since the last pass:** #8 (dismiss behavior now built).

---

## 3. Draft PR Comment for Raj

> Quick question on the streak-freeze tap, not a blocker — just want to make sure it's intentional: if the user is offline when they tap "Use streak freeze," is the confirmation (button state + toast) an optimistic local update, or does it wait on a server response?
>
> Since there's no cooldown and no restore window on this action, I want to make sure we're not in a spot where a flaky connection lets the client show "restored" twice before the server reconciles, or leaves a user seeing a confirmed freeze locally that never actually landed on their account. If there's already a pattern elsewhere in the app for this kind of optimistic-then-reconciled action, that's probably enough — just want to confirm rather than assume.
