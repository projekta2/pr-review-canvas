# Annotated example: a full review, comment by comment

A realistic, fictional review transcript on a mid-sized PR ("Add CSV export to the orders dashboard"), with the reviewer's reasoning made explicit — the part that's normally invisible because it only happens in someone's head.

---

**PR:** Add CSV export to the orders dashboard
**Diff size:** +180 / −12, 6 files
**Reviewer:** Dana

---

> **Comment 1 — on `exportOrdersToCsv()`**
>
> "This loads all orders into memory before writing the CSV. For an account with 200k orders, that's a multi-hundred-MB array sitting in memory for the duration of the request. Worth streaming rows to the response instead of building the full array first — happy to pair on this if the streaming approach isn't familiar."
>
> **Severity:** Blocking
>
> *Reviewer's reasoning:* this is a performance category item from the checklist — "no obvious unbounded resource usage." It's not visible in local testing with 50 fake orders, which is exactly why it's worth flagging explicitly rather than assuming CI or staging will catch it. The offer to pair signals this isn't a gotcha, it's a real architectural ask.

---

> **Comment 2 — on the route handler**
>
> "Is there a permission check here? I don't see one, and the existing `/orders` list endpoint checks `req.user.canViewOrders` before returning data."
>
> **Severity:** Blocking
>
> *Reviewer's reasoning:* security category — "new endpoints respect existing authorization rules." Phrased as a genuine question rather than an accusation, because it's entirely possible the check exists somewhere the reviewer hasn't seen yet (a middleware, for instance) — and indeed, in this case, it turned out to be missing.

---

> **Comment 3 — on the CSV header generation**
>
> "Nit: `headers.join(',')` will break if any field contains a comma (e.g. an address). Not blocking since this is internal-only for now, but worth a follow-up issue before this is exposed to customers directly."
>
> **Severity:** Should fix, not blocking
>
> *Reviewer's reasoning:* a real bug, but scoped correctly — it doesn't currently affect anyone because the feature is internal-only, so blocking the PR over it would be disproportionate. Explicitly saying so prevents the author from over-indexing on a comment that isn't actually urgent.

---

> **Comment 4 — on a renamed variable**
>
> "Nit: `ordersArr` → `orders` reads a little cleaner since the type is already clear from context, but genuinely don't feel strongly about this one."
>
> **Severity:** Optional
>
> *Reviewer's reasoning:* labeled explicitly as low-stakes so the author doesn't spend time agonizing over a style preference that the reviewer themselves flagged as optional.

---

**Author's response:**

> "Good catch on the permission check — that's a real gap, fixing now. On the streaming question: I hadn't worked with streaming responses before, would take you up on pairing if you have 20 minutes this week. Filed #519 for the CSV escaping issue. Renamed the variable, no objection."

*Why this response works:* it engages with each comment specifically rather than a blanket "fixed!", takes the offer to pair instead of either ignoring it or guessing at an unfamiliar pattern alone, and files a tracked issue for the deferred fix instead of letting it disappear. See [`how-to-receive-feedback.md`](../../guides/es/how-to-receive-feedback.md) for more on this pattern.

---

**Second pass, after the fixes:**

> "Streaming change looks right — confirmed it handles the 200k-row case in staging without the memory spike. Permission check is in place. Approving."

*Reviewer's reasoning:* the second pass doesn't re-review the entire diff from scratch — it verifies specifically that the two blocking issues were actually resolved, and confirms it concretely (checked staging) rather than taking the diff at face value. The optional and "should fix" items aren't re-litigated, because they were already correctly scoped as non-blocking in the first pass.

---

## What this transcript demonstrates

- **Severity was stated explicitly on every comment**, which let the author triage four comments into "two things to fix now, one to track later, one to take or leave."
- **Every blocking comment included reasoning, not just a verdict** — "for an account with 200k orders" and "the existing endpoint checks this" both give the author something concrete to act on.
- **The reviewer verified the fix, not just the intent.** "Approving" came after confirming the streaming approach actually worked at scale, not just after seeing a new commit appear.
