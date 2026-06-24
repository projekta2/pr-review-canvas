# PR Review Canvas — GitHub Projects Template

> How to set up a GitHub Project board for tracking PR reviews with the Canvas methodology.  
> Source: [projekta2/pr-review-canvas](https://github.com/projekta2/pr-review-canvas) · MIT License

---

## Overview

This template shows how to use GitHub Projects as a PR review tracker for your team. The goal: every PR that needs review has a card, every card has a structured review issue attached to it, and the board shows review status at a glance.

---

## Board Setup

### Columns

| Column | What goes here |
|--------|---------------|
| **🔍 To Review** | PRs assigned for review, not yet started |
| **👀 In Review** | Active reviews in progress |
| **💬 Changes Requested** | PR is back with the author |
| **✅ Approved** | Review complete, PR approved |
| **🔒 Merged** | Closed and done |

### Custom Fields to add

Go to your project's **Settings → Fields → New field** and add:

| Field name | Type | Options |
|------------|------|---------|
| Risk Score | Number | 0–100 |
| PR Type | Single select | `feature` / `bugfix` / `refactor` / `docs` / `security` / `infra` |
| Review Checklist | URL | — |
| Reviewer | Person | — |
| Repo | Text | — |

---

## Issue Template

Create a GitHub Issue Template in your repo at `.github/ISSUE_TEMPLATE/pr-review.md`:

```markdown
---
name: PR Review
about: Track a code review using the PR Review Canvas checklist
title: "Review: [PR title]"
labels: pr-review
assignees: ''
---

## PR Details

**PR link:** 
**Author:** 
**Risk estimate:** <!-- 0-100, 100 = highest risk -->
**PR type:** <!-- feature / bugfix / refactor / docs / security / infra -->

---

## Review Checklist

> Full interactive checklist: https://projekta2.github.io/pr-review-canvas/

### 1. Context & Scope
- [ ] PR description explains what changed
- [ ] PR description explains why it changed
- [ ] References relevant issue/ticket/spec
- [ ] Scope is appropriate
- [ ] Related changes included
- [ ] Breaking changes documented

### 2. Architecture & Design
- [ ] Fits existing patterns
- [ ] New abstractions justified
- [ ] Appropriately simple
- [ ] New dependencies justified
- [ ] API contracts well-considered

### 3. Code Quality
- [ ] Names communicate intent
- [ ] Functions do one thing
- [ ] Complex logic has explanatory comments
- [ ] Error cases handled
- [ ] No unjustified duplication
- [ ] No committed commented-out code

### 4. Testing
- [ ] Tests exist for new behavior
- [ ] Edge cases covered
- [ ] Test names describe scenarios
- [ ] Tests are independent
- [ ] Skipped tests have a reason

### 5. Performance & Security
- [ ] No obvious N+1 queries
- [ ] DB queries indexed
- [ ] Input validated and sanitized
- [ ] No hardcoded credentials
- [ ] Auth checks in place
- [ ] No sensitive data logged

### 6. Documentation
- [ ] Public APIs documented
- [ ] README updated if needed
- [ ] CHANGELOG updated
- [ ] Migration guide for breaking changes

### 7. Standards
- [ ] Passes linting and CI
- [ ] Commit messages descriptive

### 8. Final Read
- [ ] Maintainable in 6 months
- [ ] Understandable without asking the author
- [ ] PR does what the description says

---

## Review Notes

**What works well:**

**Suggestions / concerns:**

**Questions for the author:**

**Decision:**
- [ ] Approved
- [ ] Approved with minor comments
- [ ] Changes requested
- [ ] Needs discussion
```

---

## Automating the board with GitHub Actions

Add this to `.github/workflows/pr-review-board.yml` to automatically create a review issue and add it to the Project when a PR is ready for review:

```yaml
name: Create PR Review Issue

on:
  pull_request:
    types: [review_requested]

jobs:
  create-review-issue:
    runs-on: ubuntu-latest
    permissions:
      issues: write
      contents: read
    steps:
      - name: Create review tracking issue
        uses: actions/github-script@v7
        with:
          script: |
            const pr = context.payload.pull_request;
            const reviewer = context.payload.requested_reviewer?.login || 'unassigned';
            
            await github.rest.issues.create({
              owner: context.repo.owner,
              repo: context.repo.repo,
              title: `Review: ${pr.title}`,
              body: `PR: ${pr.html_url}\nAuthor: @${pr.user.login}\nReviewer: @${reviewer}\n\n<!-- Paste PR Review Canvas checklist here -->`,
              labels: ['pr-review'],
              assignees: [reviewer]
            });
```

---

## Tips for teams

**Keep risk scores honest.** A 5-line change to authentication logic should score higher than a 200-line CSS refactor. Use the PR Review Canvas [main checklist](https://projekta2.github.io/pr-review-canvas/) to calibrate.

**Use the "Changes Requested" column actively.** When you request changes, move the card. When the author pushes a fix, they move it back. The board should reflect reality.

**Link the interactive checklist.** Add `https://projekta2.github.io/pr-review-canvas/` as a bookmark in your team's GitHub Project description so reviewers can open it alongside the diff.

---

*From [PR Review Canvas](https://github.com/projekta2/pr-review-canvas) — MIT licensed.*
