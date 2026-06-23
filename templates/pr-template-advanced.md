# Pull Request Template — Advanced

> For complex, high-risk, or cross-team changes — migrations, breaking API changes, anything touching auth, billing, or infrastructure. For everyday changes, use [`pr-template.md`](pr-template.md) instead; this one is intentionally heavier.

## Summary

What does this PR do, and why does it need the extra scrutiny that justified this template?

## Context

- Issue / ticket / RFC: [link]
- Related PRs (if this is part of a series): [links]
- Stakeholders who should be aware: [team/person — and why]

## Problem

What was broken, missing, or risky before this change? Include enough detail that someone unfamiliar with the backstory understands the motivation.

## Solution

What approach did you take, and what alternatives did you consider and reject? A reviewer who knows the codebase will ask "why not X" — answer it here before they have to.

| Alternative considered | Why rejected |
|---|---|
| [Option A] | [Reason] |
| [Option B] | [Reason] |

## Scope of change

- **Systems/services touched:** [list]
- **Data migrations involved:** [yes/no — link migration if yes]
- **Backward compatibility:** [is this breaking? for whom?]
- **Feature flag / rollout plan:** [flag name, rollout percentage strategy, or "no flag, direct deploy because..."]

## How to test this

1. [Local reproduction steps]
2. [Staging verification steps]
3. [What metrics/dashboards to watch post-deploy]

## Risk assessment

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| [e.g. "Migration locks the orders table"] | [Low/Med/High] | [Low/Med/High] | [e.g. "Run during low-traffic window, tested on staging-scale data"] |

## Rollback plan

If this needs to be reverted in production, what's the actual procedure? Is reverting the deploy enough, or does the data migration need a separate down-migration?

## Checklist (author)

- [ ] I tested this against production-scale data, not just a handful of local rows
- [ ] I have a rollback plan that doesn't depend on remembering details under pressure
- [ ] I notified the stakeholders listed above before merging, not after
- [ ] Monitoring/alerting is in place for the new behavior
- [ ] I documented the breaking change (if any) in the changelog and notified affected consumers
- [ ] This was reviewed by someone outside my immediate team, if it crosses team boundaries
