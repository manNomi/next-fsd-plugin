---
name: timeboxed-assignment-operator
description: Operate a strict timeboxed frontend assignment safely, including deadline tracking, feature branch setup, trusted versus ignored tests, PR timing, no-commit-after-submit freeze, cutline decisions, and final submission readiness.
---

# Timeboxed Assignment Operator

Use this at the start of a frontend take-home assignment with a hard deadline, required branch or PR flow, ignored tests, or no-commit-after-submit rules. This is an operations skill: it protects time, submission validity, and reviewer trust.

## Hard gates

- Record the assignment start time, deadline, timezone, target branch, remote URL, and submission route before implementation planning.
- Treat deadline and submission rules as product requirements.
- If the assignment says a test is obsolete or should be ignored, do not use that test as pass/fail evidence. Record why in README or final notes.
- Prioritize submitting a truthful PR before the deadline over chasing unfinished polish.
- After PR submission, enter submission freeze: do not commit, amend, force-push, or push follow-up commits unless the assignment explicitly allows it.
- In the final 90 minutes, stop starting new major features. Focus on verification, README, PR creation, submission link, and honest residual risk.

## Setup checks

- Confirm repository is initialized.
- Confirm package manager and install/dev commands from lockfiles and scripts.
- Confirm recommended runtime versions from assignment text and local environment when possible.
- Confirm remote `origin` and target branch.
- Confirm collaborator/invitation/submission-link tasks that must be done outside code.
- Confirm which tests are trusted, stale, ignored, or missing.

## Time budget defaults

For a 24-hour assignment, use this default budget unless the user gives a different one:

- First 60-90 minutes: setup, repo scan, requirement forensics, design/API screenshots, and implementation plan.
- Next 12-14 hours: MVP feature slices.
- Next 4-5 hours: reliability states, tests, manual QA, README rationale.
- Final 90 minutes: verification, final diff scan, PR, submission link, no-commit freeze.

If time is already low, compress scope instead of skipping verification.

## Cutline rules

When time is limited, cut in this order:

1. Visual polish that does not affect requirement clarity.
2. Optional abstractions and folder purity.
3. Nice-to-have tests that do not protect core behavior.
4. Non-critical responsive refinements.

Do not cut:

- required user flows
- pricing or payload correctness
- disabled/pending duplicate action prevention
- API error handling for required submit flows
- README run instructions and known limitations
- PR creation before deadline

## Output format

### 1. Deadline and submission rules

List start time, deadline, timezone, target branch, PR/submission route, no-commit-after-submit rule, and any non-code setup tasks.

### 2. Repository setup checklist

List repo init, remote, branch, install/dev commands, runtime assumptions, and collaborator/submission tasks.

### 3. Test trust map

Classify tests as trusted, ignored by assignment, stale, missing, or manual-only. Explain ignored tests briefly.

### 4. 24-hour execution budget

Allocate time blocks for planning, MVP, reliability/tests, README, PR, and final freeze.

### 5. Feature slice plan

List slices in the order they should be implemented, with expected verification per slice.

### 6. Commit / PR checkpoints

Define when to commit, when to push, when to create PR, and when to stop committing.

### 7. Cutline rules

List what to drop first and what must not be dropped.

### 8. Final 90-minute protocol

List exact final actions: verification, README, diff scan, PR, submission link, freeze.

### 9. Submission checklist

List final checks for branch, remote, PR URL, README, verification evidence, known limitations, and no post-submit commits.

### 10. Residual risk

List unfinished work, ignored tests, manual-only checks, and any deadline risk honestly.
