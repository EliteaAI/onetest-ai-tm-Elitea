---
id: ELITEA-3741
title: "Budget Warnings — Dismissal Persistence and Isolation per Project, User, Browser and UTC Month"
priority: medium
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [r-2.0.7, enhancement:6439, eng:backend, eng:frontend, feat:admin-platform, feat:notifications, feat:settings, nfr:usability]
requirements: ["EliteaAI/elitea_issues#6439"]
---

# ELITEA-3741: Budget Warnings — Dismissal Persistence and Isolation per Project, User, Browser and UTC Month

**Module:** Usage Cost Tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a dismissal is scoped to one user, one project and one UTC month in one browser, and that keys from past months are cleaned up.

**Coverage:**
- A dismissal in project A does not affect project B, and there is no stale banner flash on switch
- A different user in the same browser is not affected
- Another browser / incognito window does not inherit the dismissal (it is stored client-side)
- UTC month rollover and pruning of stale keys

## Preconditions

- Two team projects (A and B) where the test user is over the warning threshold in both
- A second test user over the threshold in project A
- Cost Budgets mode = **enforce**; dismissal switch **ON**
- Note: the issue says "same session/period". The implementation persists in localStorage until the UTC month ends (expected behavior)

## Test Data

| Field | Value |
|-------|-------|
| Key format | `elitea.budgetWarning.dismissed.{userId}.{projectId}.{scope}.{YYYY-MM}` |
| Unrelated key | add `test.keep = 1` to localStorage manually |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As user 1, dismiss the banner in project A, then switch to project B | Project B's banner is shown; project A's banner does not flash during the switch |
| 2 | Log out, log in as user 2 in the same browser profile, and open project A | User 2 sees their own banner |
| 3 | Log in as user 1 in a different browser or an incognito window and open project A | Banner is shown again |
| 4 | Back in the first browser, edit user 1's project A key so its month part is last month (e.g. `2026-09`), add `test.keep = 1`, and reload | Banner returns; the edited stale key is removed; `test.keep` is untouched |
| 5 | Clear site data and reload | Banner is shown at the current level |

## Expected Final State

Only current-month dismissal keys remain; unrelated keys are untouched.

## Pass/Fail Criteria

**Pass:**
- Dismissals are isolated per project, user and browser
- The last-month key is ignored and pruned; other keys are untouched

**Fail:**
- A dismissal leaks to another project or user
- A stale banner flashes on project switch, or unrelated localStorage keys are removed
