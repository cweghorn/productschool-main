# Streakly Comeback Screen — Learning Synthesis & Hypothesis

*Sources: [change_log.md](../change_log.md), [decision-brief.md](../decision-brief.md) (which itself draws on interview-synthesis.md, nps-analysis.md, and competitive-matrix.md in 02-research/).*

## Learning Synthesis

### What We Know

- Day-7 retention dropped 9 points, 48% → 39%, since the streak redesign shipped, and the drop is concentrated in users who break their streak in week 1 — missing two days in a row nearly doubles churn.
- The streak reset reads as punishment and directly causes churn: Tom's interview account ("the app sent me this 'you lost your streak' notification that just made me feel bad... there was no way to recover it") is corroborated by 6 of 10 raw NPS comments citing the punishing reset or lack of recovery as their reason for disengaging or deleting the app.
- Users explicitly asked for a recovery/forgiveness mechanism by name in NPS feedback ("other apps let you freeze a streak, why not this one").
- No competitor (Duolingo, Babbel, Elevate, Mimo) has a standing, personalized, always-on comeback flow — this is genuine competitive white space, not a catch-up fix.
- Reward and forgiveness are two distinct levers pulling on two different populations: Priya's retention came from milestone *celebration* (reward, kept a 14-month power user engaged), while Tom's churn came from a lack of *forgiveness* after a slip. A fix addressing only one risks missing the other half of the problem.
- The Comeback screen concept is technically feasible with data Streakly already has — no new integrations required (per Raj).
- Persona playtesting of the built prototype (change_log.md, Day 2) showed a one-tap action preserves the intended emotional payoff for the target user (Tom) better than a reversible toggle — the interaction pattern itself, not just the underlying mechanic, affects whether the fix lands.

### What We Assume

- That an unconditional streak-freeze (no minimum streak length, no cooldown) drives comeback behavior without materially cheapening the mechanic for the broader user base — untested; the same playtest that validated the one-tap interaction also surfaced a live, unresolved concern (via the Priya persona) that an easy restore could dilute the achievement that retains long-tenure power users.
- That showing the Comeback screen every session until dismissed is the right cadence, rather than a one-time surface or a softer periodic nudge — not yet tested against alternatives, and NPS already shows this user base is sensitive to notification frequency/fatigue.
- That the same fixed screen content generalizes across users at very different tenure and streak lengths — the playtest (Amara persona, hypothetically a 4-day-tenure user) suggested a screen built around a 12-day example may not feel relevant or reassuring to someone earlier in the fragile week-1 window.
- That the Comeback screen is the single biggest lever on the Day-7 drop, as opposed to other unconfirmed contributing factors (see below).
- That 3 interviews and 10 NPS comments are representative of the broader 340K MAU base rather than a vocal minority — explicitly flagged as an open question in the decision brief, still unanswered.

### What We Still Do Not Know

- What exactly changed in the streak redesign, and whether the diagnosed pain points predate it or were introduced by it — the decision brief calls this out as an unresolved gap that also blocks fairly evaluating a rollback option.
- Whether the Day-7 drop is uniform or concentrated in specific tracks, platforms, or acquisition channels — no segment-level breakdown exists yet.
- The expected retention lift if the Comeback screen works, and how it would be measured — Success Metrics remains an open placeholder in the PRD.
- Whether a forgiveness mechanic measurably dilutes the achievement/pride dynamic that retains power users like Priya — a real, anticipated question from Marcus that the current research and playtest cannot answer on their own.
- Real-user reaction to the actual build — persona playtesting is an internal proxy; the decision brief calls for a concept/usability test with real users before committing engineering time, and that has not yet happened.
- Rollout and validation plan (concept test → A/B test against a control group) — not yet designed or run.

## Hypothesis

We believe that the Comeback screen (best-streak stat, 60-second comeback lesson, one-tap streak-freeze) will deliver higher return-and-continue rates among users who break their streak in week 1, instead of churn, for Streakly users in their first 7 days, as measured by Day-7 retention rate.
