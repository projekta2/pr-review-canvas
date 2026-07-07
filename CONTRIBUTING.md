# Contributing to PR Review Canvas Skill

Thanks for considering a contribution. This skill stays intentionally small — the value is in a fixed, reliable structure, not in accumulating every possible check.

## Good contributions

- **Language or framework-specific reference files** (e.g. `reference/react.md`, `reference/python.md`) that extend category 5 (Performance & security) or category 7 (Standards) with stack-specific checks — following the pattern of `reference/feedback-tone.md`. Keep each under ~200 lines; link out rather than duplicating general advice.
- **Refinements to the feedback-tone reference** — better question/command examples, additional severity conventions.
- **Bug reports** where the 8-category output doesn't match what's described in `SKILL.md`.
- **Translations** — if you'd like to contribute a Spanish version, open an issue first so we agree on where it lives (likely `es/SKILL.md` mirroring `pr-review-canvas`'s existing `es/` convention).

## Not a fit for this repo

- Auto-commenting / auto-posting integrations — this skill is explicitly a draft-for-a-human tool. If you want to build an auto-posting layer on top, that's a great separate project; happy to link to it from here.
- General-purpose static analysis rules unrelated to the 8-category review structure — those belong in a linter, not this skill.

## Process

1. Fork the repo
2. Create a branch
3. Make your change, keeping `SKILL.md` itself short — push detail into `reference/`
4. Open a PR describing what changed and why

## Code of conduct

Be direct, be kind. Critique the content, not the person.
