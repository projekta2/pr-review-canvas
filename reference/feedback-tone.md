# Feedback tone reference

Used by the `pr-review-canvas` skill when phrasing review findings. Drawn from the same principles as [`guides/how-to-give-feedback.md`](https://github.com/projekta2/pr-review-canvas/blob/main/guides/how-to-give-feedback.md) in the full PR Review Canvas kit.

## Prefer questions over commands when intent is genuinely ambiguous

- ❌ "This will fail if the list is empty."
- ✅ "What happens if `items` is an empty array?"

## Prefer suggestions over directives when there's a real judgment call

- ❌ "You must change this to use async/await."
- ✅ "Async/await might make this more readable here — worth it for this case?"

## Name the pattern, not just the instance, when something repeats

- ❌ "Extract this into a function." (said three separate times on three separate lines)
- ✅ "This logic appears in three places — would it make sense to extract it once?"

## Severity should be explicit, not implied by tone

Use a consistent marker per finding so the reader can triage at a glance:

- 🔴 Blocking — must be addressed before merge
- 🟡 Should address — not blocking, but should be fixed soon
- 🟢 Optional — worth mentioning, no action required

Do not rely on adjectives ("this is bad", "this seems risky") to convey severity — use the marker.

## Always end on the human decision, not just a list of findings

A list of findings without an explicit approve / approve-with-comments / request-changes recommendation forces the reader to re-derive your conclusion. State it.
