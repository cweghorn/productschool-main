# Stakeholder: Raj

## From the Workspace (directly sourced)

- **Squad & role (as documented in [01-orient/project.md](../01-orient/project.md) and [CLAUDE.md](../CLAUDE.md)):** Engagement squad, role listed as **"Data."** Constraint noted in CLAUDE.md: "no new data sources needed for the Comeback screen concept, per Raj."
- **Feasibility confirmation** ([decision-brief.md](../decision-brief.md), [strategy.md](../strategy.md), [pm-brief.md](../pm-brief.md), [docs/hypothesis.md](../docs/hypothesis.md)): Raj confirmed the Comeback screen is technically doable with data Streakly already has — no new integrations required.
- **Open items flagged directly in decision-brief.md:** eligibility logic (who qualifies to see the screen) and streak-freeze rules (how a freeze is earned, limited, applied) are both explicitly unscoped and need "engineering definition" from Raj before a real build estimate exists.
- **Role in the upcoming triad session** ([docs/triad-session.md](../docs/triad-session.md)): listed there as **"Raj (Eng)"** — owns the feasibility/abuse-cost gut check on the freeze mechanic, the build estimate, and (with Christa) the primary + guardrail metric for the eventual A/B test.

**⚠️ Role conflict, not resolved by the workspace:** earlier docs (project.md, CLAUDE.md) call Raj the squad's **data** person; the more recent triad-session doc — written per your own framing of "Raj (eng lead)" — treats him as the **engineering** owner fielding build estimates and feasibility. Nothing in the workspace explains this shift (a title change? two different Rajs? a looser use of "engineering" to mean "technical feasibility" generally?). Worth confirming which is accurate before the triad session, since it changes what he can credibly commit to in the room.

## Filled from Default Profile (not confirmed in workspace)

*Everything below came from the default profile you supplied, not from any file in this repo. Flag and correct anything inaccurate.*

- **Role:** Owns technical architecture, sprint scope, and feasibility decisions for the Streakly squad.
- **Pushes back on:** Underspecified requirements, scope that grows mid-sprint, anything touching the streak/notification pipeline without a clear rollback plan.
- **Needs before saying yes:** Clear acceptance criteria, edge cases called out upfront, a clear answer to "what does done look like."
- **Has asked before, unanswered:** "How will we know if this is working after it ships?" and "What happens if the user has never set a streak, or breaks it twice in a week?"
- **Communication preference:** Async-first, short messages, bullets over paragraphs; doesn't like being surprised in standups.
- **Open item:** Still waiting on data model clarification for the streak-freeze field. *(Note: this specific framing — "a streak-freeze field" — doesn't appear anywhere in the workspace, but it lines up with the already-documented, unscoped "streak-freeze rules" item from decision-brief.md above. Likely the same open question, described differently.)*
