# PR Review Canvas — Linear Template

> Ready-to-paste checklist for [Linear](https://linear.app) issues.  
> Source: [projekta2/pr-review-canvas](https://github.com/projekta2/pr-review-canvas) · MIT License

---

## How to use this in Linear

1. In your Linear workspace, go to **Settings → Templates → New template**
2. Set the template type to **Issue**
3. Paste the content below into the description field
4. Save as "PR Review" or similar

Alternatively, create a new issue for each PR you review and paste this directly into the description.

Linear supports standard Markdown checkboxes — they render as interactive checkboxes in Linear issues.

---

## PR Review Checklist

**PR:** <!-- Link to the PR -->  
**Reviewer:** <!-- Your name -->  
**Date:** <!-- YYYY-MM-DD -->  
**Review Readiness Score:** <!-- Count checked items / 51 -->

---

### 1. Context & Scope

- [ ] The PR description explains *what* changed
- [ ] The PR description explains *why* it changed (business or technical reason)
- [ ] The PR references the relevant issue, ticket, or spec
- [ ] The scope is appropriate — not too large, not artificially split
- [ ] Related changes are included (migrations, config updates, documentation)
- [ ] Breaking changes are explicitly documented

### 2. Architecture & Design

- [ ] The change fits the existing architectural patterns of the codebase
- [ ] New abstractions introduced are justified and not over-engineered
- [ ] The solution is appropriately simple for the problem it solves
- [ ] Dependencies added are justified (not reinventing what the stdlib provides)
- [ ] Data models and API contracts are well-considered for future extension

### 3. Code Quality

- [ ] Names (variables, functions, classes) clearly communicate intent
- [ ] Functions and methods do one thing
- [ ] Complex logic has explanatory comments (the "why", not the "what")
- [ ] Error cases are handled explicitly, not silently ignored
- [ ] No significant duplication without justification
- [ ] No commented-out code committed

### 4. Testing

- [ ] Tests exist for the new behavior
- [ ] Tests cover the edge cases, not just the happy path
- [ ] Test names describe the scenario being tested
- [ ] Tests are independent (no shared mutable state between tests)
- [ ] If tests were removed or skipped, there's a clear reason
- [ ] Manual testing steps are described if automated tests don't cover the full behavior

### 5. Performance & Security

- [ ] No obvious N+1 queries or unnecessary iterations over large datasets
- [ ] New database queries are indexed appropriately
- [ ] User input is validated and sanitized before use
- [ ] No hardcoded credentials, secrets, or API keys
- [ ] Authentication and authorization are checked where required
- [ ] No new sensitive data logged in a way that could leak it

### 6. Documentation

- [ ] Public APIs (functions, classes, endpoints) are documented
- [ ] README updated if the change affects setup, configuration, or usage
- [ ] CHANGELOG updated if this is a user-facing change
- [ ] Migration guide included for breaking changes

### 7. Standards & Process

- [ ] Code passes linting and formatting checks
- [ ] Commit messages are descriptive (not "fix", "wip", "update")
- [ ] No merge commits in the branch (rebased or squashed where appropriate)
- [ ] CI is passing

### 8. Final Read

- [ ] I would be comfortable maintaining this code in 6 months
- [ ] A new team member could understand this change without asking me
- [ ] The PR does what the description says it does
- [ ] I've looked at the diff as a whole, not just the individual files

---

## Review Notes

**What works well:**
<!-- One or more specific things done well in this PR -->

**Suggestions / concerns:**
<!-- Specific, constructive feedback -->

**Questions:**
<!-- Things I don't understand that the author should clarify -->

**Outcome:**
- [ ] Approved
- [ ] Approved with minor comments (no re-review needed)
- [ ] Changes requested
- [ ] Needs discussion before proceeding

---

*Generated from [PR Review Canvas](https://github.com/projekta2/pr-review-canvas) — free, MIT licensed.*
