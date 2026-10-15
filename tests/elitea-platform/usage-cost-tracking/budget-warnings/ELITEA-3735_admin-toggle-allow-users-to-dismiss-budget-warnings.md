---
id: ELITEA-3735
title: "Budget Warnings — Admin Toggle 'Allow Users To Dismiss Budget Warnings' Visibility, Default and Persistence"
priority: high
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [r-2.0.7, enhancement:6439, eng:backend, eng:frontend, feat:admin-platform, feat:notifications, feat:settings, nfr:usability]
requirements: ["EliteaAI/elitea_issues#6439"]
---

# ELITEA-3735: Budget Warnings — Admin Toggle 'Allow Users To Dismiss Budget Warnings' Visibility, Default and Persistence

**Module:** Usage Cost Tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that the platform-wide dismissal switch in Admin → Features → Cost Budgets is shown only when budgets are active, defaults to ON, persists, and takes effect for users without a service restart.

**Coverage:**
- Switch visibility per Cost Budgets mode (off / observe / enforce)
- Default ON state and persistence after save
- Toggling does not change mode, thresholds or limits
- Change is applied to user chats on reload, with no restart (AC3)

## Preconditions

- Admin user logged in to `{{base_url}}` with access to the Admin portal
- A regular test user whose spend is currently **at or above** the warning threshold (banner visible); Cost Budgets mode = **enforce**
- Note: the switch is **platform-wide**. There is no per-project or per-user override (expected behavior; the issue mentions per-tenant)

## Test Data

| Field | Value |
|-------|-------|
| Admin path | Admin → Features → Cost Budgets |
| Switch label | Allow Users To Dismiss Budget Warnings |
| API check | `GET {{base_url}}/api/v2/elitea_core/platform_settings` → `cost_budgets_warning_dismissible` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Admin → Features → Cost Budgets with mode = enforce | "Allow Users To Dismiss Budget Warnings" switch is shown with a hint about warnings returning at 90% / 95%; it is **ON** |
| 2 | Set mode = **off** (do not save) | The switch is **hidden** |
| 3 | Set mode = **observe**, then back to **enforce** | The switch is visible in both modes |
| 4 | Note the current limits and thresholds, turn the switch **OFF** and save | Save succeeds |
| 5 | Reload the Admin page | Switch is still OFF; mode, limits and thresholds are unchanged |
| 6 | As the test user, check `GET /api/v2/elitea_core/platform_settings` in DevTools → Network | `cost_budgets_warning_dismissible: false` |
| 7 | As the test user, **reload** the chat page | Budget banner is shown **without** a close (X) button, with no service restart |
| 8 | As admin, turn the switch back **ON** and save. In a chat the user already has open, do **not** reload; wait ~1 min | Record whether the X button appears without a reload (expected: it does not, because platform settings are fetched once per page load) |
| 9 | Reload the user's chat page | Close (X) button is back on the banner |

## Expected Final State

The switch is ON, its value is persisted server-side, and the user's banner shows a close button after reload.

## Pass/Fail Criteria

**Pass:**
- Switch hidden in mode off, visible in observe/enforce, default ON
- OFF state persists and is returned by `platform_settings`
- Close button appears/disappears after reload, with no restart
- Mode, limits and thresholds are not changed by the toggle

**Fail:**
- Switch missing, defaults to OFF, or shown in mode off
- Value lost after reload, or toggling changes other Cost Budgets settings
- A service restart is required for the change to apply
