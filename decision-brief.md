# Decision Brief: Streak Break & Week-1 Retention

*For Marcus, Head of Product. Sources: interview-synthesis.md, nps-analysis.md, competitive-matrix.md (02-research/).*

## Situation

Day-7 retention has dropped 9 points, from 48% to 39%, since the streak redesign shipped, and the drop is concentrated in users who break their streak in week 1 — most never come back. Interviews, NPS feedback, and competitive research all independently point to the same root cause: an all-or-nothing streak reset with no graceful way back in.

## Key Findings

- **The streak reset reads as punishment and directly causes churn.** Tom (churned user) described the "you lost your streak" push as making him "feel bad" with "no way to recover it." NPS corroborates this directly — 6 of 10 raw comments cite the punishing reset or lack of recovery as their reason for disengaging or deleting the app.
- **Week-1 users feel the streak's downside before any of its upside.** Priya (14-month power user) says habit formation took her ~3 weeks; Amara (day 4) is already anxious about losing progress, with none of the reward payoff banked yet. This is a structural mismatch, not a one-off complaint.
- **No competitor owns a standing, personalized comeback flow.** Duolingo and Mimo both focus on *preventing* a break (paid freezes, streak shields); Babbel and Elevate offer no recovery mechanic at all. Duolingo's only response to an already-broken streak was a one-time 2026 marketing campaign, not a permanent feature — this is genuine white space, not a "catch up to competitors" fix.
- **Notifications are a compounding problem, not the root cause.** NPS users call notifications "random" and describe turning them off; this matches Tom's experience of the harsh "lost your streak" push. Competitive research shows Duolingo leans aggressive and Babbel deliberately low-pressure, but neither adapts tone by user tenure — an unaddressed gap on both sides of the market.
- **Reward and forgiveness are two different levers, and the data splits along them.** Priya's retention came from milestone *celebration* (reward); Tom's churn came from a lack of *forgiveness* after a slip. A fix that only adds one of these will miss the other half of the problem.

## Options Considered

1. **Streak recovery/freeze mechanic** — protect the streak from breaking in the first place (matches Duolingo's paid freeze, Mimo's streak shield). Addresses prevention, but doesn't fix what happens once a break has already occurred, and isn't differentiated — competitors already do this.
2. **"Comeback screen" after a break** (best-streak stat, short comeback lesson, one-tap freeze) — the concept the team has already sketched. Directly targets the untouched white space (no competitor has a standing post-break flow) and addresses both the reward and forgiveness gap.
3. **Notification overhaul** — make reminder tone and timing adapt to user tenure instead of one blanket policy. Lower scope, addresses a real but secondary pain point (NPS + competitive both flag it), doesn't address the core punishing-reset problem on its own.
4. **Roll back the streak redesign** — could resolve the symptom quickly if the harsh notification and no-recovery behavior were introduced by this specific redesign. Not yet a fully informed option: it's undetermined whether these pain points predate the redesign or were introduced by it, and what else shipped alongside it that a rollback would also reverse. Needs confirmation from Marcus/engineering on exactly what changed before it can be properly weighed.

## Recommended Action

Build the Comeback screen (Option 2) as the primary fix, since it's the only option that addresses the root cause identified across all three research sources and occupies competitive white space no one else owns.

## Impact: Company & Customer

**Good for the customer:** this directly targets the documented pain point behind churn, not a hypothetical one — it's Tom's exact stated reason for leaving, Amara's week-1 anxiety, and the top request in NPS feedback (a forgiveness mechanic, explicitly compared to competitors). It removes an existing point of friction rather than adding a new ask of users.

**Good for the company:** Day-7 retention is the metric already in decline (48% → 39%), and Streakly's growth (28% YoY, 340K MAU) depends on holding new users past week 1 — recovering part of that drop protects the base that growth is built on. It's also one of the few fixes here that's offense, not just defense: the competitive matrix found no competitor with a standing comeback flow, so this is a differentiation opportunity, not just a retention patch.

## Feasibility

Per Raj (Engagement squad, data), the Comeback screen is technically doable with data Streakly already has — no new data sources required. Two things are still open and unscoped: **eligibility logic** (who qualifies to see the screen, and under what conditions) and **streak-freeze rules** (how a freeze is earned, limited, and applied). Both need engineering definition before a real build estimate exists — feasibility looks favorable, but isn't fully scoped yet.

## Additional Planning Needed to Move Forward

- Define **Non-Goals** and **Success Metrics** for the PRD — both are still open placeholders pending team alignment.
- Scope **eligibility logic** and **streak-freeze rules** with Raj/engineering to get a real build estimate.
- **Concept/usability test** the Comeback screen mockup with users before committing engineering time.
- Sequence an **A/B test plan** (Comeback screen vs. control) to validate impact on Day-7 retention before full rollout.
- Get **Marcus's sign-off on problem framing** — the original gating step — before any of the above moves from planning to execution.
- Confirm with Marcus/engineering **exactly what changed in the streak redesign**, to properly evaluate the rollback option above.

## Anticipated Questions from Marcus

**On the diagnosis:**
- What exactly changed in the streak redesign — can we isolate the specific change that caused the drop? *(Same gap that leaves the rollback option unresolved above.)*
- Is the drop uniform, or concentrated in specific tracks, platforms, or acquisition channels? Current research only shows it's sharpest in week-1 breakers — no segment-level breakdown exists yet.
- The interview sample is 3 users and the NPS sample is 10 comments — how confident are we this reflects the broader base and isn't a vocal minority?

**On the fix:**
- Could a forgiveness mechanic (freeze/comeback screen) dilute the achievement that retains power users like Priya — does making streaks more forgiving reduce the payoff that kept her engaged for 14 months?
- What's the actual engineering estimate once eligibility logic and freeze rules are scoped — timeline, cost, squad capacity?
- What's the expected retention lift if this works, and how would we know? *(Ties back to Success Metrics, still an open placeholder in the PRD.)*

**On sequencing and risk:**
- What's the rollout/validation plan before full launch — concept test, then A/B test against a control group?
- Is this the Engagement squad's top priority, or does it compete with other roadmap items — what's the opportunity cost?
- Is the competitive white space stable, or is there a risk a competitor closes it before Streakly ships?

*None of these are answered by the current research — they're flagged here as likely follow-ups to resolve before or during the planning steps above.*

## Why Now

The retention drop is already a 9-point hit and concentrated in the highest-leverage, most fragile window (week 1); the competitive white space is open today but not guaranteed to stay that way; and three independent research streams — user interviews, NPS, and competitive analysis — have already converged on the same diagnosis, so the team is aligned on the problem and ready to move to solution design without further validation delay.
