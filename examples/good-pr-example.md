# Annotated example: a good PR

This is a fictional but realistic PR, annotated to show *why* it works. The goal isn't to present a flawless PR — it's to show the specific, learnable habits that separate "easy to review" from "exhausting to review."

---

## Title

> **Fix race condition causing duplicate order confirmation emails**

> 🟢 **Why this works:** specific, names the actual bug, and would mean something in a changelog six months from now. Compare to a vague alternative like "fix email bug" — same change, far less useful once it's just a line in `git log`.

## Description

> **Summary**
> Orders placed within ~200ms of each other from the same session could trigger two confirmation emails, because the "has this order been confirmed" check and the "send email" action weren't atomic. This adds a database-level lock around that check.
>
> **Context**
> Closes #482. Reported by support — three customers got duplicate emails in the last week, all during checkout retries on slow connections.
>
> **What changed**
> - Added a unique constraint on `order_confirmations.order_id`
> - Wrapped the confirm-and-send logic in a transaction
> - Added a test that fires two concurrent confirmation attempts and asserts only one email is sent
>
> **How to test**
> Run `npm test -- order-confirmation.spec.ts` — the new test (`prevents duplicate confirmation under concurrent requests`) specifically exercises this.
>
> **Risks**
> Low. This only adds a constraint and a transaction boundary to an existing flow; it doesn't change the happy-path behavior for the 99.9% of orders that weren't racing.

> 🟢 **Why this works:** a reviewer can understand the entire problem, fix, and validation plan without opening a single file. The "Risks" section in particular does real work — it tells the reviewer where to focus (the new transaction logic) and where not to worry (the unaffected happy path).

## The diff (abbreviated)

```diff
+ await db.transaction(async (trx) => {
+   const existing = await trx('order_confirmations')
+     .where({ order_id: orderId })
+     .first();
+
+   if (existing) {
+     return; // already confirmed, nothing to do
+   }
+
+   await trx('order_confirmations').insert({ order_id: orderId, confirmed_at: new Date() });
+   await sendConfirmationEmail(orderId);
+ });
```

> 🟢 **Why this works:** the comment `// already confirmed, nothing to do` explains *why* the early return exists, not what it does (the code already says what — it returns). This is exactly the kind of comment that earns its place.

## The test

```ts
it('prevents duplicate confirmation under concurrent requests', async () => {
  const [resultA, resultB] = await Promise.all([
    confirmOrder(orderId),
    confirmOrder(orderId),
  ]);

  const emailsSent = await getEmailsSentTo(order.customerEmail);
  expect(emailsSent).toHaveLength(1);
});
```

> 🟢 **Why this works:** the test name describes the exact scenario it guards against. If this test fails six months from now, whoever sees the failure knows immediately what regressed, without opening the file.

## What the reviewer didn't have to do

- Ask "why was this changed" — the description answered it.
- Guess at blast radius — the "Risks" section scoped it.
- Manually verify the fix works — the new test demonstrates it directly, exercising the actual race condition rather than just checking the function doesn't throw.

That's the throughline across every "good PR": it does the reviewer's orientation work *for* them, so the actual review time goes into judging the approach, not reconstructing the context.
