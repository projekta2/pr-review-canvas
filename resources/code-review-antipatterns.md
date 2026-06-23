# Code review anti-patterns

The recurring ways code review goes wrong — on both sides of the diff. Most of these aren't about bad intentions; they're habits that feel reasonable in the moment and quietly erode trust in the process over time.

## On the reviewer's side

### The drive-by nitpick avalanche
Twenty comments, all about formatting, naming, and style, zero about whether the logic is correct. It feels thorough. It isn't — it's the easiest kind of feedback to generate, which is exactly why it's tempting, and it crowds out the comments that actually matter. **Fix:** if every comment you're about to leave is style-level, ask whether a linter should be catching this instead, and spend the saved time on one real pass for logic and edge cases.

### The rubber stamp
Approving within two minutes of a 400-line diff landing. Sometimes this is genuinely fine (a trivial change) — but when it becomes the default regardless of size, review stops providing any actual signal. **Fix:** match review depth to risk, explicitly. If you're rubber-stamping something risky because you're busy, say so: "approving but didn't review the migration logic closely, flagging for someone with more context there."

### The silent re-litigation
Blocking a PR on a preference that was already settled by the team's style guide or a previous decision, without acknowledging that it was already decided. **Fix:** if you disagree with an existing standard, raise it as a separate conversation about the standard — not as a blocker on someone else's unrelated PR.

### The vague blocker
"This doesn't feel right" with no specifics. It's technically a blocking comment, but it gives the author nothing to act on except guessing. **Fix:** if you can't articulate the concrete failure mode, that's a sign to investigate further before commenting, not after.

### Reviewing the person's history, not the diff in front of you
"Last time you did X, so I assume this has the same issue" — without actually checking whether it does this time. **Fix:** every PR gets reviewed on its own evidence. Patterns from history can inform *where to look closer*, never substitute for actually looking.

## On the author's side

### The mega-PR
A single PR that touches twelve unrelated things because they all happened to get done in the same week. Reviewable in theory, exhausting in practice — and the unrelated parts dilute scrutiny on the parts that actually matter. **Fix:** one PR, one reason. If you can't summarize the change in one sentence without "and," it's probably two PRs.

### The silent push
Pushing new commits in response to feedback with no comment explaining what changed, leaving the reviewer to diff the diff to figure out what was addressed. **Fix:** reply to each comment, even briefly. "Fixed in latest commit" costs ten seconds and saves the reviewer several minutes of detective work.

### Defending instead of engaging
Responding to every comment with a justification for the original choice, rather than engaging with whether the comment has a point. Even when the original choice was correct, "no, this is fine" teaches a reviewer that raising concerns isn't worth the friction. **Fix:** "I considered that — here's the constraint that led me here, but open to revisiting if it doesn't hold up" gets the same outcome without shutting the conversation down.

### Burying the real change in noise
Auto-formatting the entire file as part of a one-line logic fix, so the diff shows 200 changed lines for a one-line change. **Fix:** keep formatting changes in a separate commit or PR, even when it's tempting to "clean up while you're in there."

### Treating review comments as a final exam to pass
Fixing exactly what was flagged, in the narrowest way possible, without addressing the underlying pattern if it shows up elsewhere in the same file. **Fix:** if a comment points out a real issue, check whether the same issue exists nearby before declaring it fixed.

## On both sides

### Litigating tone over substance in the thread itself
A comment reads as harsher than intended, and instead of either side naming it directly, the conversation spirals into terse one-liners that get progressively colder. **Fix:** if a thread feels like it's heating up, that's the moment to switch to a quick call, not to write a sharper comment back.

### Treating the checklist as the ceiling, not the floor
Running through a checklist mechanically and stopping there, even when something checklist-shaped doesn't capture what's actually concerning about a specific change. **Fix:** a checklist exists to make sure you don't forget the routine things — it's not a substitute for actually thinking about the specific PR in front of you.
