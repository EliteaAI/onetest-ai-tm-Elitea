---
id: ELITEA-3737
title: "Budget Warnings — Non-Dismissible Banner When Admin Disables Dismissal, Stored Dismissals Ignored"
priority: high
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [r-2.0.7, enhancement:6439, eng:backend, eng:frontend, feat:admin-platform, feat:notifications, feat:settings, nfr:usability]
requirements: ["EliteaAI/elitea_issues#6439"]
---

# ELITEA-3737: Budget Warnings — Non-Dismissible Banner When Admin Disables Dismissal, Stored Dismissals Ignored

**Module:** Usage Cost Tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the admin disables dismissal, the banner has no close button at any level and can't be hidden by an earlier dismissal, and that the earlier dismissal is honored again once the switch is re-enabled.

**Coverage:**
- No close button at 80/90/95 (AC11)
- Banner persists across reload, new chat, logout/login (AC12)
- Stored localStorage dismissal ignored while OFF and honored again when ON

## Preconditions

- Logged in to `{{base_url}}` as a test user whose spend is at **80–89%** of the member limit; Cost Budgets mode = **enforce**
- Admin access to toggle "Allow Users To Dismiss Budget Warnings"; switch is initially **ON**

## Test Data

| Field | Value |
|-------|-------|
| Dismissal key | `elitea.budgetWarning.dismissed.{userId}.{projectId}.member.{YYYY-MM}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a chat in the test project and click X on the banner | Banner hidden; localStorage key = `80` |
| 2 | As admin, turn the switch **OFF** and save. As the user, reload the chat | Banner **reappears** at level 80 with **no** close button, even though the dismissal key is still in localStorage |
| 3 | Open a new chat, then log out and log back in | Banner is still shown, with no close button |
| 4 | Push spend to 90–94%, then 95–99% (reload ~60s after spending) | Banner shows elevated, then critical severity, never with a close button |
| 5 | As admin, turn the switch back **ON** and save. As the user, reload | If spend is still at the dismissed level, the banner is hidden again (the stored value was kept); at a higher level it shows with a close button |

## Expected Final State

Switch is ON and the banner follows the normal dismissal rules again.

## Pass/Fail Criteria

**Pass:**
- No close button at any level while OFF
- While OFF, the banner can't be hidden by reload, new chat, logout/login or an earlier dismissal
- Earlier dismissal is honored again after switching back ON

**Fail:**
- Close button visible while OFF, or banner hidden by a stored dismissal
- Dismissal state lost after toggling OFF → ON
