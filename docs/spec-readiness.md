# Spec Readiness Review — Streakly Comeback Screen

*Reviewed in-character as Raj (per [stakeholders/raj.md](../stakeholders/raj.md)) against [decision-brief.md](../decision-brief.md), [docs/hypothesis.md](hypothesis.md), [docs/triad-session.md](triad-session.md), and [docs/codebase-summary.md](codebase-summary.md). 2026-09-16.*

**⚠️ Update, later the same day:** the "no cooldown, no minimum streak length, no restore window" decisions below were reversed after this review — the 7-day minimum and 90-day cooldown were reinstated, and a home/acknowledgment screen was added back in front of the Comeback screen. Sections 2 and 3 below reflect the reinstated rules. See change_log.md for both the original removal and this reversal, including the tradeoff this reintroduces for users who match Tom's profile (see stakeholders/raj.md discussion above — Raj's original sign-off was conditional on the no-limits version).

## 1. Readiness Summary

### What was solid going in

- **Problem framing was fully evidenced and already signed off.** The Day-7 retention diagnosis (interviews, NPS, competitive research, Marcus's sign-off) didn't need to be relitigated — no pushback here.
- **The high-level feature shape was consistent everywhere it appeared:** best-streak stat, 60-second comeback lesson, one-tap streak-freeze. No conflicting descriptions across docs.
- **The interaction design had already been pressure-tested.** The persona playtest (change_log.md, Day 2) caught and fixed a real UX issue — a toggle undercutting the "gift" moment — before this review even started.
- **Streak model resolved cleanly once asked:** one streak per account, not per track.

### What needed work — decided live in this conversation, not written anywhere beforehand

- **Streak-freeze data model** (field type, where it lives) — not documented anywhere; extracted verbally, and only settled after multiple passes.
- **The break/eligibility trigger** — the exact threshold (missed days before the Comeback screen appears) actually changed mid-conversation (2 days → 1 day), meaning it wasn't a settled decision walking in.
- **Whether the freeze is automatic or requires explicit user action** — unspecified; this materially changes whether the freeze button does anything at all. Resolved: it's explicit (frozen only when the button is tapped).
- **The restore window** — initially set to a 30-day timeout, then removed: the restore is available regardless of how much time has passed since the break. This directly resolves the edge case below.
- **Resolved:** a user who returns after any length of time — including someone matching the exact target persona (broke a streak, didn't reopen the app for a while) — retains the restore option. No time-based cutoff.
- **Resolved:** users with zero streak history (never had a streak to break) are explicitly out of scope for this feature.

### Bottom line

Raj's verdict: workable, no remaining logical contradictions or open questions — conditional on all of the above actually being written into the spec, not left as decisions made verbally in a thread.

---

## 2. Rewrite: Eligibility & Streak-Freeze Mechanics

*Replaces the "unscoped" placeholder in decision-brief.md and the vague "one-tap streak-freeze offer" line in pm-brief.md.*

> **Trigger:** A user who breaks a streak sees an acknowledgment home screen (not a blank reset), with a path into the Comeback screen. The Comeback screen persists every session until the user acts (freeze and/or lesson) or dismisses it — dismissing returns to the home screen and the offer reappears next session.
>
> **Streak-freeze data model:** A single account-level streak counter (one streak per account, not per track). On break, the counter is *not* automatically reset or automatically frozen — it enters a pending/restorable state. It is only frozen at its pre-break value when the user explicitly taps "Use streak freeze."
>
> **Eligibility: 7-day minimum, 90-day cooldown.** The freeze is only offered if the broken streak was 7+ days *and* the user hasn't used a freeze in the last 90 days. A user who doesn't meet both conditions sees an explanatory message in place of the freeze offer, with no way to bypass it. *(Reinstated after this review — see the update note at the top of this doc.)*
>
> **No restore window.** A broken streak remains restorable via the freeze (or continuable via completing the comeback lesson) indefinitely — there is no time-based cutoff after which the offer expires, regardless of how long it's been since the break. *(This one was not reversed — still no timeout.)*
>
> **Combinable actions:** A user can use the freeze and complete the comeback lesson independently, in either order. Completing the lesson alone is sufficient to continue the streak (no freeze required); using the freeze alone restores the prior count without advancing it for the current day.
>
> **Out of scope:** Users with zero streak history (never had a streak to break) are not eligible for this flow — there is nothing for them to restore or freeze.

---

## 3. Async Slack Message — Scope Confirmation Before Sprint Kickoff

> Hey Raj — heads up before you build: scope changed after our last pass. Here's where things actually landed:
>
> - Added a home/acknowledgment screen in front of the Comeback screen — dismissing the Comeback screen returns here, and it reappears next session
> - Freeze eligibility is back to a 7-day minimum streak length *and* a 90-day cooldown between freezes — not the "no limits" version we closed out last time
> - Freeze: account-level streak, one per account (not per track); frozen only when the user taps the button — not automatic
> - No restore window — that part didn't change, the offer still never expires regardless of how long it's been since the break
> - Freeze and the comeback lesson are independent; either can be done alone, or both
> - Users with zero streak history are explicitly out of scope — nothing to restore, so nothing to build for them here
>
> I know the 7-day/90-day limits were the thing we specifically removed last time because they'd exclude our actual target user — that tradeoff is back on the table intentionally, not a mistake. Wanted you to hear the reversal directly before it hits a ticket, not find it mid-sprint.
