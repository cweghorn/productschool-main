# Streakly — Recovery Strategy

## The Drop

Day-7 retention fell 9 points, from 48% to 39%, since the streak redesign shipped. The drop is sharpest among users who break their streak in week 1 — missing two days in a row nearly doubles churn.

## Hypothesis

Users go passive because breaking a streak feels like failure and there's no graceful comeback. Today, a streak reset gets no acknowledgment (same home screen, counter back to zero), and the "lost your streak" push notification has a harsh tone and offers no path back. A comeback needs to feel specific to the user's own progress — not a generic "keep going!" nudge.

## Direction Being Explored

A "Comeback screen" shown when a streak breaks: best-streak stat, a 60-second comeback lesson, and a one-tap streak-freeze. Per Raj, technically doable with existing data sources — open items are the eligibility logic (who sees it) and freeze rules.

## Status

Not yet decided. Problem alignment (with Marcus) comes before solutioning.
