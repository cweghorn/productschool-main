# Streakly — Change Log

## Day 1 — 2026-09-14 — Discovery Phase Kickoff

- Identified Day-7 retention drop: 48% → 39% since the streak redesign shipped.
- Framed hypothesis: streak breaks feel like failure, with no graceful comeback path.
- Sketched initial direction: "Comeback screen" concept (best-streak stat, comeback lesson, streak-freeze).
- Next: align with Marcus on problem framing before solutioning.

## Day 2 — 2026-09-16 — Comeback Screen Prototype (prototype/index.html)

- **Change:** Reverted the streak-freeze control from a toggle switch back to a one-tap button ("Use streak freeze") with a permanent "✓ Streak restored" confirmation state.
- **Why:** Ran a persona playtest (Tom, Amara, Priya) against the current build. Tom — the exact target user (churned after a 12-day streak break) — reacted well to the mechanic itself but flagged that a reversible toggle switch feels like adjusting a setting, not receiving something back. Since the whole point of this feature is the emotional payoff of that moment for users like Tom, this was judged the single highest-priority fix over Amara's concern (the 12-day example doesn't scale to her 4-day reality) and Priya's concern (an easy restore risks diluting the achievement that retains 14-month power users like her) — both real, but longer-term/strategic rather than an immediate failure at the feature's core moment.
- **Kept from prior round:** freeze and lesson remain independently usable in either order; completing the lesson alone still continues the streak and makes the freeze button show "Not needed — you're already back."
- **Not yet addressed (flagged for a future round):** Amara's personalization gap (hardcoded 12-day example shown to a hypothetical 4-day-tenure user) and Priya's achievement-integrity concern (no distinction between an earned streak and a restored one).

## Day 3 — 2026-09-16 — Problem Framing Signed Off

- Marcus signed off on the problem framing (Day-7 retention drop, streak-break-as-punishment diagnosis). This clears the gating step decision-brief.md flagged as required before any solutioning work.

## Day 4 — 2026-09-16 — Spec Readiness Review with Raj (docs/spec-readiness.md)

- **Context:** Ran an in-character spec review as Raj (per stakeholders/raj.md) against decision-brief.md and the docs/ set. Surfaced that the streak-freeze data model, break trigger, and freeze-automaticity were never actually written down — only decided verbally in this review.
- **Change 1 — removed the 30-day restore window.** Initially proposed as a timeout on how long a broken streak stays restorable, then removed: the freeze and comeback lesson remain available regardless of how long it's been since the break.
- **Why:** The 30-day cutoff would have excluded users who match the exact target persona — someone who breaks a streak and doesn't reopen the app for a while (Tom's profile). A timed cutoff on the feature's own primary use case was judged not worth the tradeoff.
- **Change 2 — users with zero streak history are explicitly out of scope.** There's nothing for them to restore or freeze, so this flow doesn't apply to new users who've never had a streak to break.
- **Resolved:** the review's one remaining open question (freeze is only frozen on explicit user action, not automatic on break) was confirmed and is otherwise unchanged from Day 2.

## Day 5 — 2026-09-16 — Design Review with Lena, Celebration Screen Added (docs/design-review.md, prototype/index.html)

- **Context:** Ran an in-character design review as Lena (per stakeholders/lena.md) against the prototype and interview-synthesis.md. Confirmed Amara's day-4 personalization gap (flagged Day 2) was still unresolved — early-tenure users were still getting the same break-recovery template as Tom, just with a smaller number.
- **Change 1 — added an independent celebration screen** (`screen-celebration` in prototype/index.html) for early-tenure users on an active, unbroken streak. Unlike the Comeback screen, it's not tied to any break — it's a standing positive touchpoint.
- **Why:** Per interview-synthesis.md, week-1 users feel the streak's risk before its reward; reusing the break-recovery template for someone who hasn't broken anything (Amara) doesn't address that. A separate screen that doesn't require failing first does.
- **Change 2 — copy correction caught in review.** First draft ("Great job! You're on fire. Keep going!") was flagged as the exact generic pattern strategy.md warns against. Replaced with "Day 4. Showing up 4 days in a row is the hardest part of building this — and you're already doing it." — grounded in Priya's quote that most people quit before the habit forms.
- **Change 3 — added a scenario switcher** to the prototype so both flows (Tom's Comeback screen, Amara's Celebration screen) can be reviewed side by side in one file.
- **Not yet resolved:** the celebration screen's copy and visual design are a first draft, not signed off by Lena in an actual review — flagged explicitly in docs/design-review.md rather than presented as final.

## Day 6 — 2026-09-16 — Reinstated Home Screen and Freeze Eligibility Limits

- **Change:** Reversed two Day 2 decisions and one earlier removal, by direct instruction: (1) added back a home/acknowledgment screen in front of the Comeback screen, with a "Not right now" dismiss path that returns to it and reappears next session; (2) reinstated the 7-day minimum streak length and 90-day cooldown on the streak-freeze (previously removed during the initial interview, before Day 1 of this log).
- **Why:** Direct product decision — not driven by new research or a stakeholder review this time. Flagged before implementing: the 7-day/90-day limits were originally removed specifically because they'd exclude users matching Tom's profile (the primary target persona — breaks a streak and doesn't reopen the app for a while), and Raj's spec readiness review (Day 4) was explicitly conditional on the no-limits version. This reintroduces that exact tradeoff intentionally.
- **Implementation:** Freeze eligibility (7+ day streak, no freeze in the last 90 days) is now modeled in prototype/index.html with an explanatory message shown when a user doesn't qualify, plus a demo-only preview toggle to simulate the ineligible state without needing real multi-session account data.
- **Updated for consistency:** pm-brief.md, prototype/README.md, and docs/spec-readiness.md (which now carries an explicit update note, since it previously documented Raj's sign-off on the opposite rule).
- **Not yet done:** docs/qa-checklist.md was written against the pre-reversal build and is now stale on two points (the dismiss-path finding, and the zero-history exclusion check) — not updated in this pass.
