# How to receive review feedback without taking it personally

Most code review advice is written for reviewers. This one's for the other side of the diff — because how you respond to feedback shapes whether your reviewers keep giving you honest, useful comments or start softening everything to avoid a reaction.

## The comment is about the code at the time you wrote it

Not about your skill, your intelligence, or your worth as an engineer. Code review comments are a snapshot: this is what was visible in this diff, today. Reading "this function is doing too much" as "I am bad at my job" is a jump the comment itself never made — that interpretation gets added on your end, and it's worth catching yourself doing it.

## Separate "they found a real issue" from "they're judging me"

These are two different facts, and only one of them needs a reaction:

- **A real issue was found.** Useful information. Fix it, or explain why it's not actually an issue.
- **A judgment about you was made.** Sometimes this genuinely happens (see the note on actual hostility below), but far more often it's a read you're adding to a neutral comment because feedback is uncomfortable by default, even when delivered well.

If you notice yourself reacting defensively, it's worth pausing before replying — a comment written in the first wave of defensiveness rarely improves the conversation.

## When you disagree

Explain your reasoning, don't just push back. "I considered that, but X constraint meant Y approach wouldn't work — happy to walk through it if useful" moves the conversation forward. "No, this is fine" doesn't give the reviewer anything to engage with, and it reads as dismissive even if that's not how you meant it.

It's fine to disagree and hold your position. It's also fine to be wrong and say so directly — "good catch, missed that" costs nothing and builds the kind of trust that makes reviewers comfortable being direct with you in the future.

## When feedback feels like a lot all at once

A PR with fifteen comments can feel like a pile-on, especially if you're newer or it's a big change. A few things that help:

- **Sort by severity first**, if your reviewer didn't already. Some comments are blocking, some are "consider this," some are nitpicks. Treating all fifteen as equally urgent is exhausting and usually wasn't the intent.
- **Respond to clusters, not each comment in isolation**, when several comments point at the same root cause. "I see the same issue flagged in three places — I'll refactor the shared helper rather than patching each call site" is often a better fix than three individual patches.
- **It's okay to say "this is a lot, can we sync briefly instead of going comment by comment."** Review threads aren't the only valid medium, and sometimes they're the slowest one.

## On genuinely hostile or dismissive feedback

Sometimes feedback really is delivered badly — sarcastic, condescending, or personal rather than technical. That's worth naming directly, separate from the technical content: "I'll address the technical points, but the phrasing in [comment] read as dismissive — can we keep feedback focused on the code?" You don't have to absorb that silently to seem professional; naming it clearly and calmly *is* the professional response. See [`how-to-give-feedback.md`](how-to-give-feedback.md) — it's worth sharing with whoever's giving you that kind of feedback.

## Treat review comments as free senior-engineer time

Reframe: someone spent real time reading your code closely enough to find that edge case. That's not free anywhere else — pairing time, mentorship, code-quality coaching, all cost something. A thorough review is one of the cheapest ways to get better at this job, even when (especially when) it points out something you missed.

## What to do after you've addressed the comments

Reply explicitly to each one — "Fixed in [commit]," "Good point, changed to X," or "Disagree, here's why, let me know if that changes things" — rather than silently pushing new commits and leaving the reviewer to guess what changed and why. It's a small habit that makes the second review pass dramatically faster.
