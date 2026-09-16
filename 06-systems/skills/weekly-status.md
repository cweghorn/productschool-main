---
name: weekly-status
description: "Turn raw bullet-point notes into a formatted leadership status update with Shipped, In Progress, Blockers, and Next Week sections. Use whenever the user asks for a weekly status update, leadership update, or status report, or pastes in rough notes and asks to turn them into an update."
---

# Weekly Status Update

## Purpose

Convert raw, informal bullet-point notes into a clean, leadership-ready weekly status update. The output should be scannable in under a minute — leadership doesn't need the detail, they need the headline.

## Input

The user provides raw notes: rough bullets, fragments, or a stream-of-consciousness list of what happened, what's in progress, what's stuck, and what's coming. Notes may be unsorted — sort them into the right section based on content, not on where the user happened to mention them.

## Output Structure

Always exactly four sections, in this order:

1. **Shipped** — what was completed and delivered this week.
2. **In Progress** — what's actively being worked on, not yet done.
3. **Blockers** — what's stuck, and (if the notes say why) what's blocking it.
4. **Next Week** — what's planned to start or continue next week.

### Rules

- Maximum 3 bullets per section. If the notes have more than 3 relevant items for a section, keep the 3 most significant and drop or merge the rest — don't invent a summary bullet that papers over dropped items.
- If a section has nothing in the notes, write "Nothing to report" rather than omitting the section or inventing content.
- Plain, declarative language. Short sentences. State what happened — no jargon, no buzzwords, no hedging language ("we're hoping to," "should probably").
- Never add information, numbers, or outcomes that weren't in the user's notes. If a note is vague, keep it vague rather than filling in specifics.
- One bullet = one fact. Don't combine multiple updates into a single run-on bullet.

## Example

**Input notes:**
"finished the comeback screen mockup, raj pulled the retention data cuts, still waiting on eng estimate for streak freeze, lena's interviews are stuck bc no user list from support, next week we present to marcus"

**Output:**

**Shipped**
- Comeback screen mockup complete.
- Retention data cuts pulled and reviewed.

**In Progress**
- Waiting on engineering estimate for streak-freeze logic.

**Blockers**
- User interviews stalled — no user list from support yet.

**Next Week**
- Present findings to Marcus.
