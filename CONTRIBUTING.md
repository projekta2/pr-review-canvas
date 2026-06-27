# Contributing to PR Review Canvas

Thanks for considering a contribution. This project stays useful because reviewers with different experiences add what's missing from their own day-to-day — that's the whole point of it being open.

## Start here: tasks you can finish today

If you've never contributed to an open-source project before, or you just want something concrete to pick up without having to read the whole codebase, these are real gaps that need filling — each one takes 20–30 minutes:

| Task | File to edit | What to do |
|---|---|---|
| Add a checklist item you've actually used | [`checklists/pr-review-checklist.md`](checklists/pr-review-checklist.md) | Add the item under the right category + one sentence explaining the failure mode it prevents |
| Fix a phrase that feels vague or preachy | [`guides/how-to-give-feedback.md`](guides/how-to-give-feedback.md) | Replace it with a concrete example from a real review (anonymized) |
| Translate a file to your language | Any file under `checklists/`, `guides/`, `templates/`, `resources/`, or `examples/` | Mirror the file under `<folder>/<lang-code>/` (e.g. `guides/es/`) keeping the filename identical |
| Add Linear, Jira, or GitHub Projects template | `resources/linear-template.md`, `resources/jira-template.md`, `resources/github-projects-template.md` | Adapt the checklist format to the tool's native structure |
| Report a broken link or typo | Anywhere | Open an issue — no PR needed |

Pick one. Open a PR. That's it.

## All the ways to contribute

You don't need to touch code to contribute meaningfully here.

- **Add a checklist item** you wish someone had told you about, with a one-line "why."
- **Sharpen a feedback phrase** in [`guides/how-to-give-feedback.md`](guides/how-to-give-feedback.md) — real examples from real reviews (anonymized) are especially welcome.
- **Translate a file.** If you add a language, mirror the existing file structure under a `<folder>/<lang-code>/` folder (e.g. `guides/es/`) and keep filenames identical so links still resolve.
- **Add a team template** for a workflow this kit doesn't cover yet (e.g., reviewing infrastructure-as-code, reviewing data pipeline changes, reviewing design-system PRs).
- **Report what's wrong.** A checklist item that doesn't hold up, a broken link, a typo — all fair game for an issue.

## Before you open a PR

1. **Check existing issues and PRs first** to avoid duplicate work.
2. **Keep checklist items atomic.** One concrete, checkable thing per line — if it needs "and," it's probably two items.
3. **Every new checklist item needs a "why."** An instruction without a reason is just an opinion. Explain the failure mode it prevents.
4. **Match the existing tone.** Direct, specific, no fluff. "Tests verify behavior, not implementation details" is the bar — not "Make sure your tests are good."
5. **If you're touching `checklists/interactive-checklist.html`**, test it in an actual browser before opening the PR — it has no build step, so what you see is what ships.

## Opening the PR

This repo eats its own dog food: please use [`templates/pr-template.md`](templates/pr-template.md) as the basis for your PR description. Yes, that's slightly meta. That's also the point.

## Style guide for prose files

- Sentence case for headings, not Title Case.
- Active voice. "Run the tests" not "Tests should be run."
- No emoji inside guide bodies — they're fine in the README and table headers, but guides should read like a colleague explaining something, not a slide deck.
- Keep examples concrete. "Don't write `if (x == null || x == undefined)`" beats "avoid loose equality issues."

## Code of conduct

Be the reviewer you'd want reviewing your own code: direct about the problem, generous about the person. Disagreement about technical approaches is welcome and expected. Personal attacks, dismissiveness, or gatekeeping based on someone's experience level are not, and maintainers will close threads that go that direction.

## Questions

Open a [discussion or issue](https://github.com/projekta2/pr-review-canvas/issues) — there's no separate mailing list or chat for this project, on purpose, so the reasoning stays visible to everyone who finds the repo later.
