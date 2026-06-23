# Reviewing at scale: techniques for experienced reviewers

Once you're reviewing ten or more PRs a week, the bottleneck stops being "do I know what to look for" and starts being "how do I do this without it eating my whole day." This is the guide for that stage.

## Triage before you review

Not every PR deserves the same depth of attention. Before reading a single line, classify it:

- **Trivial** (typo, copy fix, dependency bump with no behavior change): skim and approve. Spending ten minutes here is a cost, not diligence.
- **Routine** (a feature following an established pattern in the codebase): review at normal depth, but you can move fast because you already know what "right" looks like for this kind of change.
- **High-stakes** (touches auth, billing, data migrations, or a system you don't fully understand): slow down deliberately. This is where the [advanced PR template](../templates/pr-template-advanced.md) earns its weight, and where it's worth pulling in a second reviewer.

Misclassifying a high-stakes change as routine is the most common way bad code ends up in production with a green checkmark next to it.

## Read the diff stats before the diff

`+1200 −40` across 30 files is a different review than `+40 −12` across 2 files, even if both claim to do "the same kind of thing." If a PR's size doesn't match its stated scope, that's worth a comment before you even start reading — either the description is incomplete, or the PR is doing more than it should.

## Review in passes, not once

Trying to catch architecture issues, naming nitpicks, and security concerns in a single read-through is how reviewers miss things. Two fast passes beat one slow one:

1. **Structural pass:** does this belong where it is, is it the right size, does the approach make sense? Don't comment on naming or style yet.
2. **Detail pass:** now go line by line for correctness, edge cases, naming, tests.

This also keeps you from anchoring on the first issue you spot and missing the bigger structural one three files later.

## Delegate review, don't just distribute it

On larger teams, "everyone reviews everything" doesn't scale and "the senior person reviews everything" doesn't scale either — it just moves the bottleneck. What does scale:

- **Domain ownership.** The person who owns a module reviews changes to it by default; others review for things outside that domain (naming, tests, general code health).
- **Pairing reviewers with context, not seniority.** A mid-level engineer who shipped the original feature often reviews a related change better than a senior engineer seeing it cold.
- **Time-boxing review SLAs**, not review depth. "Respond within 4 hours" is a healthy norm. "Find every issue" as an SLA just produces rushed, shallow reviews disguised as thorough ones.

## Use tooling to handle what tooling is good at

Linting, formatting, type-checking, and basic security scanning belong in CI, not in a human's attention span. If you're leaving the same comment about formatting more than twice, that's a CI gap, not a review failure.

The same logic applies one level up: triage itself can be partially automated. Tools like **[PR Focus AI Pro](https://chromewebstore.google.com/detail/pr-focus-ai-pro/ememaiabefeojkccjclglcmbjmdpnaoe)** sit in the browser alongside GitHub's own UI and surface a risk summary and a suggested reading order *before* you open the diff — useful for exactly the triage step above, especially once you're juggling more PRs than you can hold context on at once. It's deliberately not trying to replace your judgment on the high-stakes pass; it's there for the part of the job that's repetitive pattern-matching.

## Know when to stop reading and start talking

If a PR needs more than two or three rounds of comments to converge, the async back-and-forth has stopped being efficient. A 15-minute call resolves in real time what would take two more days of comment threads — and it's a much better signal to the author that you're trying to help them ship, not just finding fault from a distance.

## Calibrate, don't just enforce

A checklist or style guide is a starting point, not scripture. If you find yourself blocking a PR over something the checklist says but that doesn't actually matter for this specific change, say so and move on. Reviewers who apply rules without judgment train authors to game the checklist instead of writing good code.
