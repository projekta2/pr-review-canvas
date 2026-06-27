# PR Review Canvas — Jira Template

> Ready-to-paste checklist for [Jira](https://www.atlassian.com/software/jira) issues.  
> Source: [projekta2/pr-review-canvas](https://github.com/projekta2/pr-review-canvas) · MIT License

---

## Jira-specific notes

**Checkboxes in Jira:** Jira Cloud supports Markdown-style checkboxes (`- [ ]`) in issue descriptions when using the text editor (not the visual editor). Switch to "Text" mode before pasting.

**Jira Wiki Markup users:** If your Jira instance uses Wiki Markup instead of Markdown, checkboxes are not natively supported. Use `(x)` for "done" and `( )` for "not done" as visual indicators.

**Recommended setup:** Create a Jira Issue Template in your project (Project Settings → Issue Templates) with this content so it auto-populates for new review issues.

---

## PR Review Issue Template

**Paste this into a new Jira issue when starting a PR review.**

---

**PR link:** [link]  
**PR author:**  
**Reviewer:**  
**Review date:**  

---

### 1. Context & Scope

- [ ] PR description explains what changed
- [ ] PR description explains why it changed
- [ ] References the relevant Jira ticket or spec
- [ ] Scope is appropriate — not too large, not artificially split
- [ ] Related changes included (migrations, config, docs)
- [ ] Breaking changes explicitly documented

### 2. Architecture & Design

- [ ] Change fits existing architectural patterns
- [ ] New abstractions are justified (not over-engineered)
- [ ] Solution is appropriately simple for the problem
- [ ] New dependencies are justified
- [ ] Data models and API contracts considered for future extension

### 3. Code Quality

- [ ] Names clearly communicate intent
- [ ] Functions do one thing
- [ ] Complex logic has explanatory comments (the "why", not the "what")
- [ ] Error cases handled explicitly
- [ ] No significant duplication without justification
- [ ] No committed commented-out code

### 4. Testing

- [ ] Tests exist for new behavior
- [ ] Edge cases covered, not just happy path
- [ ] Test names describe the scenario
- [ ] Tests are independent (no shared mutable state)
- [ ] Removed/skipped tests have a clear reason
- [ ] Manual testing steps described if automated tests don't cover it

### 5. Performance & Security

- [ ] No obvious N+1 queries or unnecessary large iterations
- [ ] New DB queries indexed appropriately
- [ ] User input validated and sanitized
- [ ] No hardcoded credentials or API keys
- [ ] Auth checks in place where required
- [ ] No sensitive data in logs

### 6. Documentation

- [ ] Public APIs documented
- [ ] README updated if setup/usage changes
- [ ] CHANGELOG updated for user-facing changes
- [ ] Migration guide included for breaking changes

### 7. Standards & Process

- [ ] Passes linting and formatting checks
- [ ] Commit messages are descriptive
- [ ] CI is passing

### 8. Final Read

- [ ] I'd be comfortable maintaining this in 6 months
- [ ] A new team member could understand this without asking
- [ ] PR does what the description says it does
- [ ] Reviewed the diff as a whole

---

**What works well:**

**Suggestions / concerns:**

**Questions:**

**Decision:**
- [ ] Approved
- [ ] Approved with minor comments
- [ ] Changes requested
- [ ] Needs discussion

---

*From [PR Review Canvas](https://github.com/projekta2/pr-review-canvas) — MIT licensed.*
