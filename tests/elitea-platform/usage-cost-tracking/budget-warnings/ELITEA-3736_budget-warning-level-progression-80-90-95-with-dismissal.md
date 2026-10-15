---
id: ELITEA-3736
title: "Budget Warnings — Banner Escalates 80 → 90 → 95 After Dismissal and Calls Are Refused Before 100%"
priority: high
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
size: L
tags: [r-2.0.7, enhancement:6439, eng:backend, eng:frontend, feat:admin-platform, feat:notifications, feat:settings, nfr:usability]
requirements: ["EliteaAI/elitea_issues#6439"]
---

# ELITEA-3736: Budget Warnings — Banner Escalates 80 → 90 → 95 After Dismissal and Calls Are Refused Before 100%

**Module:** Usage Cost Tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that with dismissal enabled, a dismissed banner stays hidden within its level but reappears with stronger severity at 90% and 95%, and that further calls are refused once the next call's estimated cost no longer fits in the remaining budget.

**Coverage:**
- No banner below the threshold
- Levels 80 / 90 / 95 with warning / elevated / critical severity (AC7, AC9, AC14)
- Dismissal stored per level and held across reload / new chat (AC15)
- Skipped level shows the highest reached level
- Refusal can happen **below** 100% displayed spend (the gate refuses when spent + reserved + estimate > limit). The block message itself is covered by ELITEA-3676

## Preconditions

- Logged in to `{{base_url}}` as a test user; admin switch "Allow Users To Dismiss Budget Warnings" = **ON**
- Cost Budgets mode = **enforce**; per-member warning threshold = **80** (default)
- Test user has a **small member limit** in the test project (e.g. $0.10) so a few chat messages move spend through 80/90/95%
- DevTools open: Network (`budget_warning` request) and Application → Local Storage
- Note: the backend caches the warning for 60s and the page polls every 300s. **Reload ~60s after each spend step** to see the new level. Only settled spend counts toward the %, not in-flight reservations

## Test Data

| Field | Value |
|-------|-------|
| Chat message | "Hi" (a short prompt keeps each call's cost small) |
| API | `GET {{base_url}}/api/v2/elitea_core/budget_warning/prompt_lib/{projectId}/budget_warning` |
| Banner selector | `[data-testid="budget-warning-banner"]`, attribute `data-severity` |
| Dismissal key | `elitea.budgetWarning.dismissed.{userId}.{projectId}.member.{YYYY-MM}` (UTC month) |

| Spend range | Expected `level` | Expected `data-severity` |
|-------------|------------------|--------------------------|
| < 80% | null (no banner) | — |
| 80–89% | 80 | warning (amber) |
| 90–94% | 90 | elevated (amber, strong orange border) |
| 95–99% | 95 | critical (red) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | With spend below 80%, open a chat in the test project | No banner; API returns `should_warn: false`, `level: null` |
| 2 | Send messages until spend is 80–89%, wait ~60s, reload | Banner shown with the correct %, `level: 80`, `data-severity="warning"`, and a close (X) button with tooltip "Dismiss budget warning" |
| 3 | Click X | Banner hides immediately; the localStorage key for the member scope = `80` |
| 4 | Reload, then open a new chat, while still at 80–89% | Banner stays hidden |
| 5 | Send messages until spend is 90–94%, wait ~60s, reload | Banner **reappears** with `level: 90`, `data-severity="elevated"` (stronger border than step 2) |
| 6 | Click X | Banner hides; stored value = `90` |
| 7 | Send messages until spend is 95–99%, wait ~60s, reload | Banner **reappears** with `level: 95`, `data-severity="critical"` (red) |
| 8 | Click X, reload | Banner stays hidden |
| 9 | Keep sending "Hi" until a message is refused | The response says "The budget for shared models has been reached". **Record the % shown** on Settings → Usage at that moment. A refusal below 100% is expected when the next call's estimate does not fit |
| 10 | Skipped level: with a fresh user or project, go from < 80% straight to 90–94% in one step, reload | Banner shows `level: 90` (elevated), not 80 |

## Expected Final State

Each level produced a banner of increasing severity, every dismissal held until the next level, and the user is now refused further shared-model calls.

## Pass/Fail Criteria

**Pass:**
- Levels, severities and stored dismissal values match the Test Data table
- A dismissed banner stays hidden within its level across reload/new chat and reappears at the next level
- Skipping 80 shows level 90 directly
- The refusal message is shown once the budget can no longer cover the next call

**Fail:**
- Banner reappears within the same level after dismissal, or does not reappear at 90/95
- Wrong level or severity for the spend range
- Calls still succeed after spend reaches 100%
