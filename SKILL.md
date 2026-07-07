---
name: pr-review-canvas
description: Use when reviewing a pull request, diff, or set of code changes — especially Chrome/browser extensions (Manifest V3) or projects integrating a BYOK (bring-your-own-key) AI provider — and you want a structured, category-by-category review instead of an unstructured skim. Walks the change through 8 categories (context, architecture, code quality, testing, performance & security, documentation, standards, final read) drawn from a 51-item human review checklist. Produces a draft review a human edits and sends — this skill does not auto-comment on PRs, and does not require any API key or paid service to run.
---

# PR Review Canvas — structured pull request review

## The problem this solves

Most AI-assisted code review either (a) dumps every possible nitpick with no prioritization, or (b) gives a vague "looks good" summary that skips the parts a human would actually flag. This skill applies a fixed, opinionated review structure — the same one used by [PR Review Canvas](https://github.com/projekta2/pr-review-canvas), a free 51-item human review checklist — so the output is consistent across reviews and every category gets deliberate attention, not just the files that happen to catch the eye.

This skill is a **review aid for a human**, not an autonomous approval/rejection system. It never posts comments on a PR by itself; it produces a structured draft the person reviews, edits, and sends. It also runs entirely offline — no API key, no external service, no telemetry. Same BYOK-friendly philosophy as the products it comes from.

## When to use this skill

- Reviewing a pull request or diff before approving or requesting changes
- Auditing a batch of changes for a release
- Onboarding a new reviewer who wants a repeatable structure to follow
- **Reviewing a Chrome/Firefox/Edge extension change** — see [`reference/chrome-extension-mv3.md`](reference/chrome-extension-mv3.md) for MV3-specific checks most general review skills skip entirely (permissions scope, remote code loading, message-passing trust boundaries, storage handling)
- **Reviewing a change that adds or touches BYOK / bring-your-own-key AI integration** — see [`reference/byok-ai-integration.md`](reference/byok-ai-integration.md) for key-handling and provider-trust checks

## The 8-category walk

Work through the diff in this fixed order. Skip a category explicitly (state why) rather than silently omitting it — silent omission is how real bugs slip through.

1. **Context** — What problem is this PR solving? Does the PR description match what the diff actually does? Flag mismatches between stated intent and actual change.
2. **Architecture** — Does this change fit the existing structure, or does it bolt on a special case? Does it introduce a new pattern where an existing one already covers the need?
3. **Code quality** — Naming, duplication, dead code, unclear control flow. Prefer flagging the *pattern* over the *line* when the same issue repeats.
4. **Testing** — Are the changed code paths actually covered? A green CI badge is not the same as meaningful test coverage — check what the new/changed tests actually assert.
5. **Performance & security** — N+1 queries, unbounded loops, secrets in code, injection surface, auth/permission changes. Treat any change touching auth, payments, or data export as higher scrutiny by default. If the diff touches a `manifest.json`, a `content_scripts` entry, or anything under a `background`/`service_worker` path, switch to [`reference/chrome-extension-mv3.md`](reference/chrome-extension-mv3.md) for this category instead of the generic pass. If the diff touches API key storage, a settings/options page, or a provider adapter (OpenAI/Groq/Anthropic/Ollama-style), switch to [`reference/byok-ai-integration.md`](reference/byok-ai-integration.md) instead.
6. **Documentation** — Do docstrings, README sections, or API docs need updating alongside this change? A behavior change without a doc update is a review finding, not a nitpick.
7. **Standards** — Lint/format conformance, project-specific conventions (check `CONTRIBUTING.md` or `CLAUDE.md` if present in the repo for house style).
8. **Final read** — Read the diff once more top to bottom as if you were the person who has to debug this at 2am in six months. Anything that made you pause goes in the review.

## Optional: run the pattern scanner first

Before the manual 8-category walk, you can run [`scripts/scan_diff.py`](scripts/scan_diff.py) against a diff to get a fast, deterministic pre-flight list of common red flags (hardcoded secrets, `eval`/remote script loading, overly broad extension permissions, `innerHTML` with unescaped input). This is a dumb pattern scanner, not a substitute for the categories above — treat its output as candidates to verify manually, not as findings to report as-is.

```bash
python3 scripts/scan_diff.py path/to/diff.patch
# or, from inside a git repo:
git diff main... | python3 scripts/scan_diff.py -
```

## Output format

Produce a structured review with this shape, ordered by category:

```
## PR Review — <short description>

### Context
- ...

### Architecture
- ...

### Code quality
- ...

### Testing
- ...

### Performance & security
- ...

### Documentation
- ...

### Standards
- ...

### Final read
- ...

### Summary
One of: Approve / Approve with comments / Request changes — with a one-line reason.
```

Within each category, use plain, specific language tied to file:line where possible. Prefer a question over a command where the intent is genuinely ambiguous (e.g. "What happens if this list is empty?" rather than "Add a null check") — this keeps the review collaborative rather than adversarial, matching the tone guidance in [`reference/feedback-tone.md`](reference/feedback-tone.md).

If a category has nothing to flag, write "Nothing to flag" rather than omitting the heading — this is what makes the review auditable and distinguishes "I checked and it's fine" from "I forgot to check."

## What this skill does not do

- It does not post comments to GitHub, GitLab, or any PR directly. Output is a draft for the human to review and send.
- It does not replace domain-specific security or performance tooling — it's a structured pass plus a lightweight pattern scanner, not a static analyzer or SAST tool.
- It does not assume the reviewer is a beginner or an expert; the same 8 categories apply either way, just with different depth per category.
- It does not require any API key, account, or network call to function — the scanner in `scripts/` runs fully offline against a local diff.

## Related

- Full checklist, guides, and templates (Notion, Linear, Jira, GitHub Projects): [github.com/projekta2/pr-review-canvas](https://github.com/projekta2/pr-review-canvas)
- The companion tool that surfaces this same review discipline directly inside the GitHub PR inbox: [PR Focus Pro](https://github.com/projekta2/pr-focus-landing)
- The engineering decisions behind both, written up as they happen: [Build Logs](https://github.com/projekta2/build-logs)
