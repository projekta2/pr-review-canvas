# A guide for your first code reviews

You've just been assigned your first PR to review, and you have no idea where to start. That's normal — nobody is born knowing how to review code, and most teams never actually teach it. They just expect you to pick it up by watching other people's comments. This guide is the thing nobody sat you down and explained.

## Before you read a single line of code

Read the PR description first, fully, before opening the diff. If there isn't one, or it's too thin to understand what's going on, that's already useful information — ask the author for context before you start, rather than guessing.

Ask yourself: what problem is this solving? If you can't answer that in one sentence, you're not ready to judge whether the solution is good. Go find out — read the linked issue, ask in chat, whatever it takes.

## How to actually read the diff

Don't read it top to bottom in file order. GitHub's default ordering is often alphabetical, which has nothing to do with how the change makes sense. Instead:

1. **Find the entry point.** Where does the new behavior actually start — a new function, a new route, a new component? Start there.
2. **Follow the logic, not the file list.** If the entry point calls into a helper, go read the helper next, even if it's three files away in the diff.
3. **Read tests last, on purpose.** Tests tell you what the author thinks the code does. Read the implementation first and form your own opinion about what it should do — then check the tests against that, not the other way around.

## What to look for, roughly in order

1. **Does this do what the description says?** Sounds obvious, but it's the most-skipped step. A PR can be well-written, clean, and tested, and still not actually solve the stated problem.
2. **Is it in the right place?** A perfectly good piece of logic in the wrong layer (business logic in a view, a database query in a utility function) creates problems later even if it works today.
3. **Are the edge cases handled?** Empty list, zero, negative numbers, null, the network call that fails halfway through. The happy path almost always works; this is where bugs actually hide.
4. **Is it tested in a way that means something?** A test that just checks the function ran without throwing isn't really testing anything.
5. **Could you maintain this in six months?** If the answer is "only if the original author explains it to me again," that's worth raising.

You don't need to check all of this with equal depth on every PR. A one-line copy fix doesn't need the same scrutiny as a new payment flow. Match your effort to the risk.

## How not to feel overwhelmed

- **You don't have to catch everything.** Review is one layer of defense, not the only one. CI, tests, and staging exist too.
- **It's fine to approve with comments.** "This looks good, one small suggestion below, not blocking" is a completely valid review. Not everything needs to block a merge.
- **It's fine to say "I don't have enough context to review this part."** Pretending to understand something you don't helps nobody, least of all you.
- **Ask questions instead of guessing.** "Why did you choose X over Y here?" reads very differently from "This should be Y instead" when you're not actually sure which is right — and it opens a conversation instead of starting an argument.

## Giving your first comments

Comment on the code, not the person. "This function handles three different responsibilities" is a fact about the code. "You always overcomplicate things" is an attack on the person, even if unintentional. See [`how-to-give-feedback.md`](how-to-give-feedback.md) for a deeper guide on phrasing.

A useful template for your first few comments:

> *Observation* — what you noticed.
> *Why it matters* — the actual consequence, not just "it's not how I'd do it."
> *Suggestion* — what you'd consider instead, framed as a question if you're not 100% sure.

Example: "This loop re-fetches the user on every iteration (observation). With a list of 1,000 items that's 1,000 extra queries (why it matters). Would it work to fetch once before the loop and pass it in? (suggestion, as a question, since there might be a reason I'm missing)."

## When you're not sure if something is a real problem

Ask, don't assert. "Is there a reason this isn't cached?" is honest and invites an answer. "This should be cached" assumes you already know the constraints the author was working under — and sometimes you don't.

## What "approving" actually means

An approval is a statement that you reviewed this and you'd be comfortable being associated with it going to production. It doesn't mean you found every possible issue — it means you did a genuine, honest review at the level of scrutiny the change deserved. If you skimmed a section because you ran out of time or context, say so instead of approving silently.

Run through [`pr-review-checklist.md`](../checklists/pr-review-checklist.md) on a couple of PRs. It'll feel slow at first. It gets fast.
