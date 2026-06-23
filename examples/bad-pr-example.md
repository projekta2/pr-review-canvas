# Annotated example: a bad PR (and how to fix it)

Same underlying change as [`good-pr-example.md`](good-pr-example.md) — a fix for duplicate confirmation emails — but written the way it actually shows up in the wild. Every issue below is common, not exotic.

---

## Title

> **fix bug**

> 🔴 **The problem:** tells a reviewer (and future `git log` reader) nothing. Is it the email bug, the checkout bug, the login bug?
> 🟢 **Fix:** name the actual behavior and the actual symptom: "Fix race condition causing duplicate order confirmation emails."

## Description

> *(empty)*

> 🔴 **The problem:** an empty description forces the reviewer to reconstruct intent entirely from the diff. This alone roughly doubles review time, because every "why" question that a sentence could have answered now has to be inferred or asked in a comment thread.
> 🟢 **Fix:** even three sentences — what broke, why, and what changed — would have prevented most of the back-and-forth this PR generated in review.

## The diff (abbreviated)

```diff
+ const existing = await db('order_confirmations').where({ order_id: orderId }).first();
+ if (existing) return;
+ await db('order_confirmations').insert({ order_id: orderId, confirmed_at: new Date() });
+ await sendConfirmationEmail(orderId);
```

> 🔴 **The problem:** this *looks* like the same fix as the good example, but it isn't — the check and the insert aren't wrapped in a transaction. Two concurrent requests can both pass the `if (existing) return` check before either one inserts, which is exactly the race condition this PR claims to fix. Without the description explaining the intended mechanism, this is much harder for a reviewer to catch, because there's no stated claim to verify it against.
> 🟢 **Fix:** wrap the check-and-insert in a database transaction (or use a unique constraint that the insert can rely on), the way the good example does. The description should also state explicitly that atomicity is the mechanism, so a reviewer knows exactly what to verify.

## Tests

> *(none added)*

> 🔴 **The problem:** "fixed a race condition" with no test that exercises concurrency is an unverified claim. The fix might work by luck in manual testing and still fail under real production load.
> 🟢 **Fix:** a test that fires two concurrent confirmation attempts and asserts exactly one email was sent — the same one in the good example — would have caught the missing transaction immediately, before a human reviewer needed to spot it by reading carefully.

## Commit history on this PR

```
wip
fix
actually fix it
fix lint
```

> 🔴 **The problem:** none of these commit messages are useful in isolation. `git blame` on this code in a year will point to a commit called "fix" with no context.
> 🟢 **Fix:** either squash into one well-described commit before merge, or write commit messages that stand on their own: "Add transaction around order confirmation check-and-insert."

## Size

> This PR also modified 14 unrelated files — a dependency bump, a couple of formatting changes in unrelated components, and a typo fix in a different feature's copy.

> 🔴 **The problem:** scope creep. A reviewer now has to figure out which of the 14 files are actually relevant to "fix the race condition," and any one of those unrelated changes could hide an unrelated bug that gets rubber-stamped because the PR is "about" something else.
> 🟢 **Fix:** split into separate PRs. "One PR, one reason" makes both review and rollback dramatically simpler — if the dependency bump breaks something, you don't want it tangled up with a production incident fix.

---

## The pattern across all of this

Every issue here is fixable with effort the *author* spends before opening the PR, not effort the reviewer spends catching it afterward. That's the actual lesson: a bad PR doesn't usually mean bad code — it usually means the packaging (description, scope, tests, commits) didn't do the work of making the good code reviewable.
