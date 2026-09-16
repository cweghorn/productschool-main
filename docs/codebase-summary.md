# Habitica Codebase Summary — For the Streakly Comeback Screen Spec

*Source: [github.com/HabitRPG/habitica](https://github.com/HabitRPG/habitica), cloned and read directly (shallow clone, main branch, 2026-09-16). Used as a reference codebase to pressure-test how the Comeback screen feature (best-streak stat, 60-second comeback lesson, one-tap streak-freeze) would map onto a real, mature habit-tracking app's architecture — not Streakly's actual codebase.*

**Note on the repo itself:** Habitica's README currently states public PR submissions are paused (as of Aug 4, 2026) and that the project does not accept AI-generated code in contributions. Irrelevant to reading the code for research purposes, but worth knowing if anyone on the team ever considered this repo as more than a reference.

---

## 1. PM-Level Tour

**What it does, in one sentence:** Habitica is an open-source habit and task tracker that turns your real-life habits, dailies, and to-dos into an RPG — you level up a character by completing them, and lose HP when you skip them.

**How the codebase is organized:**

| Folder | What it does |
|--------|--------------|
| `website/server` | Node/Express REST API (`api-v3`, `api-v4` controllers) + Mongoose/MongoDB models. The backend of record. |
| `website/common` | Shared game-logic library used by **both** server and client — task scoring rules, the daily cron template, item/spell content definitions. Exists because the client does optimistic local scoring that the server then re-validates; the rules have to be defined once and shared. |
| `website/client` | Vue 3 single-page app — components, pages, router, store. |
| `migrations/` | One-off scripts for evolving the MongoDB schema/data (run via `migration-runner.js`). |
| `test/` | Test suites. |
| Root (`Dockerfile`, `kubernetes/`, `Procfile`, `.ebextensions`) | Deployment config — this app has shipped across Docker, Kubernetes, and Heroku at different points. |

**The 3 most important files for a PM to know:**

1. **[`website/server/models/task.js`](https://github.com/HabitRPG/habitica/blob/develop/website/server/models/task.js)** — defines what a Habit/Daily/Todo/Reward *is*, including the `streak` field. This is the single source of truth for the core loop's data shape.
2. **[`website/common/script/ops/scoreTask.js`](https://github.com/HabitRPG/habitica/blob/develop/website/common/script/ops/scoreTask.js)** — the logic that runs every time a task is checked or unchecked: streak increment/reset, XP/GP rewards, the streak-milestone achievement. This file encodes what "success" and "failure" mean in the product.
3. **[`website/server/libs/cron.js`](https://github.com/HabitRPG/habitica/blob/develop/website/server/libs/cron.js)** — the daily job that runs at each user's configured day-start: applies HP damage for missed Dailies and resets streaks. This is the literal mechanism behind a real "you lost your streak" moment.

*(Honorable mention: `website/server/models/user/schema.js` — the User model is effectively a full RPG character sheet: stats, buffs, notifications, preferences, party/guild refs, purchase history, all in one document.)*

**Key data models, and what they reveal about product decisions:**

- **User** — one giant document combining account data *and* game-character data. Tells you identity and game-character are the same object in this product; there's no separation between "your account" and "your avatar."
- **Task** (Habit/Daily/Todo/Reward, via Mongoose discriminators off one base schema) — `streak` lives **on the task**, not on the user. Tells you streaks are scoped to one specific recurring Daily, not to the account as a whole — a user with 5 Dailies has 5 independent streak counters, with no existing aggregate "my current streak" concept.
- **Group / Challenge** — tasks can belong to a shared challenge or party. Challenge/group tasks are explicitly excluded from the existing streak-protection mechanic (see below). Tells you shared/social tasks are deliberately treated with different rules than personal ones.
- **UserNotification** — an enumerated, append-only in-app notification feed, separate from `PushDevice` (mobile push tokens) and email. Tells you notification delivery is multi-channel and gated by a shared type-enum — adding any new notification means registering a new type that every channel has to handle.
- **Spells / content** (`website/common/script/content/spells.js`) — defines consumable class abilities, including an existing streak-protection spell (see below). Tells you Habitica already solved "protect my streak" once — through RPG progression (you earn it by leveling a class), not as a universal safety net. That's a materially different product philosophy than Streakly's proposed always-available freeze.

---

## 2. Mapping the Comeback Screen to This Codebase

**Where it would live:**
- **Client:** a new Vue component/page — most naturally near `website/client/src/components/tasks/` (where the existing per-task streak badge and the "Chilling Frost" spell UI already live) or a new top-level page if it's meant to be account-wide.
- **Server:** a new controller action (alongside `controllers/api-v3/tasks.js`), a new `ops/` function analogous to `scoreTask.js` (e.g. a `restoreStreak.js`), and a schema change to store a "best streak" value that doesn't exist anywhere today.
- **Notifications:** a new `NOTIFICATION_TYPES` enum entry plus new push/email templates — there is currently **no** "you lost your streak" notification type in this codebase at all (see flag below).
- **Cron:** `website/server/libs/cron.js` is where a streak actually breaks; any "did this user just break a streak" eligibility check hooks in at or immediately after this point.

**What it would touch or depend on:**
- `Task` model + `scoreTask.js` (streak increment/reset logic)
- `cron.js` (the daily reset — the actual trigger point for a break)
- The existing spell/buff system (`user.stats.buffs.streaks`, cast via the "Chilling Frost" spell) — a real precedent engineers will bring up unprompted
- `UserNotification` model + push/email delivery
- The existing streak-achievement UI (`components/achievements/streak.vue`) — adjacent, and a likely source of user confusion between "you hit a milestone" and "you're being offered a comeback"

**Blast radius — what could break:**
- `cron.js` runs for every active user, every day, and controls HP loss, streak resets, and quest progress. It is one of the highest-risk files in the entire codebase to modify — a bad hook here doesn't fail gracefully, it risks corrupting stats for the whole user base in one deploy.
- Task-scoring logic is duplicated across client (optimistic UI) and `common` (shared/authoritative) — new logic added to only one side risks the client showing a restored streak the server doesn't agree with.
- Because streak is per-task, not per-account, "restore my streak" is ambiguous by default: restore **one** Daily's streak, or something aggregated across all of a user's Dailies? Pick wrong and the feature either does something meaningless (fixes one streak out of many) or requires touching every Daily a user owns — a much bigger blast radius than it first appears.
- Challenge/group tasks are explicitly carved out of the existing streak-protection mechanic. If the new feature doesn't carry the same exclusion, a user could "restore" a streak on a shared challenge task in a way that affects other members or a leaderboard.

---

## 3. What Would Affect How I Write the Spec

**Data that doesn't exist yet:**
- **No "best streak" / "longest streak" field anywhere** — on the task or the user. The entire premise of showing someone their best-ever streak requires a new field and a decision about backfilling it for existing users (there's no historical maximum currently tracked, only the live counter).
- **No account-level "current streak" concept at all.** Habitica's streak is inherently per-Daily-task. Before this can be scoped, the spec has to resolve whether "streak" means one specific task or a new aggregate computed across a user's Dailies — that decision changes almost everything else about the ticket.
- **No "streak lost" notification type exists today.** Somewhat surprising given the premise of the feature (replacing a harsh existing notification) — in this codebase, streaks just silently reset with no explicit "you lost it" event fired at all. That event would need to be built, not just changed.

**Existing constraints to call out in the ticket:**
- A conceptually similar mechanic already ships today — Chilling Frost, a Wizard-class, level-14-gated, single-cast spell that protects *all* of a user's Dailies for one cron cycle. State explicitly why the new feature is additive to (or a replacement for) this, because engineers will ask.
- `cron.js` is shared, high-blast-radius infrastructure — any change touching it should be assumed to carry a larger review/test bar than a typical feature, and that should be reflected in the estimate.
- Streak-protection is explicitly disabled for challenge/group tasks today; the spec needs to state whether the new feature follows that precedent or intentionally diverges from it.

**The one thing engineers will ask that I should answer before scheduling kickoff:**

> "Is 'streak' here one specific task's streak, or an account-level number we have to invent?"

Everything else — data model changes, blast radius, migration needs, even the rough size of the estimate — depends on the answer. Walking into kickoff without it will stall the meeting on question one.
