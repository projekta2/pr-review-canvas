# How to give feedback that actually helps

The same technical observation can land as helpful or as hostile depending entirely on how it's phrased. This guide is about the phrasing — the technical judgment is yours, the delivery is what this can actually teach.

## The core shift: comment on the artifact, not the author

Compare these two ways of saying the same thing:

- "You always make these functions too complicated."
- "This function handles fetching, validation, and formatting — splitting it into three would make each one independently testable."

The first is a verdict on the person. The second is a fact about the code with a concrete next step. The author can argue with the second one on its merits. The first one only invites defensiveness, because there's nothing technical to respond to — it's a character judgment.

## A pattern that works for most feedback: observe, explain, suggest

1. **Observe** — state what you see, neutrally. "This loop calls the API once per item."
2. **Explain the consequence** — why it matters, concretely. "With a 1,000-item list, that's 1,000 sequential requests."
3. **Suggest, without mandating** — offer a direction, leave room for the author's judgment. "Would batching these into a single request work here, or is there a constraint I'm missing?"

That last clause — "or is there a constraint I'm missing" — matters more than it looks. It signals you're open to being wrong, which is usually true: you don't have the full context the author has. It also makes it easy for the author to say "actually yes, here's why" without it feeling like backing down.

## Calibrate by severity

Not every comment needs the same weight. Being explicit about how serious you consider something saves a lot of back-and-forth:

- **Blocking:** "This will throw on an empty array — needs a fix before merge."
- **Should fix, not blocking:** "Worth fixing, but I won't hold up the PR for it — your call on whether to do it now or follow up."
- **Nitpick / optional:** "Nit: `userList` reads a bit clearer than `ul` here, but not a big deal either way."

Labeling severity stops authors from having to guess which comments are actually load-bearing.

## Phrases that work

- "Help me understand why..." — genuinely curious, not rhetorical.
- "What happens if..." — invites the author to walk through an edge case themselves, which often surfaces the answer (or the gap) faster than you stating it.
- "Small thing, but..." — flags something as low-stakes before the author reads the rest of the sentence defensively.
- "I might be missing context here, but..." — useful exactly when you suspect there's a reason, and you want to ask rather than assume there isn't.

## Phrases to retire

- "This is wrong." — Wrong how? Be specific about the actual failure mode instead of issuing a verdict.
- "Why would you do it this way?" — Reads as rhetorical even when it isn't meant to be. "What led you to this approach?" asks the same thing without the implied judgment.
- "Obviously this should..." — If it were obvious, it's unlikely the author missed it. "Obviously" usually just signals impatience, not clarity.
- "Per my last comment..." — If a point needs repeating, the first version probably wasn't clear enough, or the disagreement is real and worth a real conversation, not a passive-aggressive callback.

## On the "compliment sandwich"

The classic advice — wrap criticism between two compliments — works fine in small doses but falls apart at scale: receive enough of them and the compliments start reading as filler, which actually undermines the genuine ones. A better default is to lead with genuine, specific praise when it's earned ("the error handling here is really thorough") and skip it when it isn't, rather than manufacturing a positive note just to soften every comment.

## When you disagree with the approach, not just the details

Separate "this has a bug" from "I would have built this differently." The first is worth raising directly. The second is worth raising as a question, because architectural disagreement is often about trade-offs neither side has fully stated yet: "I'd have leaned towards composition over inheritance here — was there a specific reason this needed the shared base class?"

## Matching feedback to experience level

A junior author benefits from more context per comment — not because they need things "dumbed down," but because they haven't yet built the pattern library a senior engineer uses to fill in gaps automatically. "This will leak memory because the listener is never removed" teaches something. A senior author reviewing the same code might only need "listener leak in the unmount path" — they'll fill in the rest, and over-explaining can read as condescending.

## The test for any comment before you post it

Would you be comfortable saying this exact sentence out loud, in the same tone, if the author were sitting next to you? If the phrasing only works because there's a screen between you, rewrite it.
