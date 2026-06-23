---
title: PR Review Checklist
tags: [code-review, checklist, engineering]
source: https://github.com/projekta2/pr-review-canvas
---

> [!info] How to use
> Save this as a new note in your vault (e.g. `Templates/PR Review Checklist.md`). If you use the Templater or core Templates plugin, set it as a template so a fresh, unchecked copy gets created per PR. Tasks below are written as standard `- [ ]` so they work with the core Obsidian task search and the Tasks plugin if you have it installed.

# 📋 PR Review Checklist

## 1. Context & Purpose
- [ ] The PR description clearly states what changed and why #context
- [ ] The PR links to the relevant issue, ticket, or spec #context
- [ ] The PR's size matches its stated scope #context
- [ ] The title is specific enough to be useful in a changelog #context
- [ ] You understand the problem this PR solves before reading the code #context

## 2. Architecture & Design
- [ ] The change fits the existing architecture, or justifies deviating from it #architecture
- [ ] Responsibilities are placed in the right layer or module #architecture
- [ ] No new pattern is introduced when an existing one already solves it #architecture
- [ ] Coupling is minimized between unrelated modules #architecture
- [ ] The abstraction level matches the problem #architecture
- [ ] Naming reflects domain concepts, not implementation details #architecture
- [ ] Consistent with similar problems solved elsewhere in the codebase #architecture
- [ ] New dependencies have a justified trade-off #architecture

## 3. Code Quality
- [ ] Functions do one thing, and the name says what that thing is #quality
- [ ] No dead code, commented-out blocks, or debug statements #quality
- [ ] Names are descriptive without being verbose #quality
- [ ] Error handling is explicit, not silently swallowed #quality
- [ ] No magic numbers or strings without a named constant #quality
- [ ] Duplication is avoided, but not at the cost of readability #quality
- [ ] Control flow is easy to follow #quality
- [ ] The diff is reviewable in scope and size #quality
- [ ] Comments explain why, not what #quality
- [ ] Edge cases are visibly handled #quality
- [ ] No reliance on implicit, fragile behavior #quality
- [ ] Formatting matches the project's conventions #quality

## 4. Testing
- [ ] New behavior has new tests, not just passing old ones #testing
- [ ] Tests verify behavior, not implementation details #testing
- [ ] At least one test covers the unhappy path #testing
- [ ] Tests are deterministic #testing
- [ ] Bug fixes include a regression test #testing
- [ ] Test names describe the scenario #testing

## 5. Performance & Security
- [ ] No obvious N+1 queries or loops over large collections #security
- [ ] User input is validated before touching anything sensitive #security
- [ ] Secrets and credentials are not hardcoded or logged #security
- [ ] New endpoints respect existing authorization rules #security
- [ ] No new attack surface without a clear mitigation #security
- [ ] Memory and resource usage is bounded #security
- [ ] Third-party data is treated as untrusted #security
- [ ] Hot-path changes show evidence performance was considered #security

## 6. Documentation
- [ ] Public functions/endpoints have docs where intent isn't obvious #docs
- [ ] README or API docs updated if usage changed #docs
- [ ] Breaking changes are called out explicitly #docs
- [ ] Config/env variable changes are documented #docs
- [ ] New dependencies have a one-line note on why #docs

## 7. Standards Compliance
- [ ] Follows the team's style guide and ADRs #standards
- [ ] CI checks pass, and you read why, not just that it's green #standards
- [ ] Commit messages are useful out of context #standards
- [ ] Accessibility basics respected for user-facing changes #standards

## 8. Final Considerations
- [ ] You'd be comfortable being paged about this at 3am #final
- [ ] Feedback is about the code, not the person #final
- [ ] If you didn't fully review something, you said so #final

---

> [!tip] Full reference
> Explanations for every item, plus a live interactive version with a progress score, live at [PR Review Canvas](https://github.com/projekta2/pr-review-canvas).
