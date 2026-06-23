# PR Review Checklist (Notion import)

> **How to import:** In Notion, create a new page, then paste this entire block of text directly into it. Notion auto-converts `#` headings, `- [ ]` lines into to-do blocks, and `>` lines into callouts. Once pasted, turn the top-level headings into a Notion database if you want one checklist row per PR.

---

# 📋 PR Review Checklist

> Use the toggle lists below to keep each category collapsible. Check items off per review; duplicate this page for your next PR if you want a fresh copy each time instead of resetting checkmarks.

## 1. Context & Purpose
- [ ] The PR description clearly states what changed and why
- [ ] The PR links to the relevant issue, ticket, or spec
- [ ] The PR's size matches its stated scope
- [ ] The title is specific enough to be useful in a changelog
- [ ] You understand the problem this PR solves before reading the code

## 2. Architecture & Design
- [ ] The change fits the existing architecture, or justifies deviating from it
- [ ] Responsibilities are placed in the right layer or module
- [ ] No new pattern is introduced when an existing one already solves it
- [ ] Coupling is minimized between unrelated modules
- [ ] The abstraction level matches the problem
- [ ] Naming reflects domain concepts, not implementation details
- [ ] Consistent with similar problems solved elsewhere in the codebase
- [ ] New dependencies have a justified trade-off

## 3. Code Quality
- [ ] Functions do one thing, and the name says what that thing is
- [ ] No dead code, commented-out blocks, or debug statements
- [ ] Names are descriptive without being verbose
- [ ] Error handling is explicit, not silently swallowed
- [ ] No magic numbers or strings without a named constant
- [ ] Duplication is avoided, but not at the cost of readability
- [ ] Control flow is easy to follow
- [ ] The diff is reviewable in scope and size
- [ ] Comments explain why, not what
- [ ] Edge cases are visibly handled
- [ ] No reliance on implicit, fragile behavior
- [ ] Formatting matches the project's conventions

## 4. Testing
- [ ] New behavior has new tests, not just passing old ones
- [ ] Tests verify behavior, not implementation details
- [ ] At least one test covers the unhappy path
- [ ] Tests are deterministic
- [ ] Bug fixes include a regression test
- [ ] Test names describe the scenario

## 5. Performance & Security
- [ ] No obvious N+1 queries or loops over large collections
- [ ] User input is validated before touching anything sensitive
- [ ] Secrets and credentials are not hardcoded or logged
- [ ] New endpoints respect existing authorization rules
- [ ] No new attack surface without a clear mitigation
- [ ] Memory and resource usage is bounded
- [ ] Third-party data is treated as untrusted
- [ ] Hot-path changes show evidence performance was considered

## 6. Documentation
- [ ] Public functions/endpoints have docs where intent isn't obvious
- [ ] README or API docs updated if usage changed
- [ ] Breaking changes are called out explicitly
- [ ] Config/env variable changes are documented
- [ ] New dependencies have a one-line note on why

## 7. Standards Compliance
- [ ] Follows the team's style guide and ADRs
- [ ] CI checks pass, and you read why, not just that it's green
- [ ] Commit messages are useful out of context
- [ ] Accessibility basics respected for user-facing changes

## 8. Final Considerations
- [ ] You'd be comfortable being paged about this at 3am
- [ ] Feedback is about the code, not the person
- [ ] If you didn't fully review something, you said so

---

> 💡 Full explanations for every item, plus an interactive web version with a progress score: [github.com/projekta2/pr-review-canvas](https://github.com/projekta2/pr-review-canvas)
