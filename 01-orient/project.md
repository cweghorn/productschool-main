# Streakly — Project Overview & PRD Skeleton

## What Streakly Is

Streakly is a consumer habit + micro-learning app that helps people learn a skill in five minutes a day. Users pick a track, complete a short daily lesson, and build a streak — the streak is the core habit loop. Launched 4 years ago, Series B funded ($42M), 2.1M registered users, 340K MAU, growing 28% YoY on MAU.

## Squad

Engagement squad — Christa (PM), Raj (data), Lena (user research).

## Current Phase

Discovery — diagnosing the Day-7 retention drop (48% → 39%) since the streak redesign shipped, before designing any solution.

## Key Stakeholders

- Marcus — Head of Product
- Raj — Data, Engagement squad
- Lena — User Research, Engagement squad
- Christa — PM, Engagement squad (you)

---

## PRD Skeleton: Streak Comeback Experience

*Draft from Slack thread. Starting point for Thursday discussion — not final.*

### Problem Statement

Day-7 retention dropped from 48% to 39% following the streak redesign launch. The drop is sharpest among users who break their streak in week 1 — once someone misses two days in a row, churn is nearly double.

Root cause hypothesis: breaking a streak feels like failure, and there's no graceful way back in.
- When a streak resets, the app shows no acknowledgment — same home screen, counter back to zero.
- The "you lost your streak" push notification has a harsh tone and offers nothing when tapped — it just drops users back at day zero.
- Users go passive because there's no path back that feels specific to their own progress (vs. a generic "keep going!" message).

### Goals

- Give users who break a streak a comeback path that feels specific to their own progress, not a generic re-engagement nudge.

### Non-Goals

*Not yet discussed in the thread — to be defined Thursday.*

### Success Metrics

*Not yet discussed in the thread — to be defined Thursday.*

---

**Open questions raised in thread (for Thursday discussion):**
- Is the core problem the streak reset itself, the notification tone, or both?
- Proposed direction to evaluate: a "Comeback screen" shown on streak break — best-streak stat, a 60-second comeback lesson, and a one-tap streak-freeze. Raj notes this is technically doable with existing data sources; open items are the eligibility logic (who sees it) and freeze rules.
