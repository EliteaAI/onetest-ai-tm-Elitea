---
id: ELITEA-0022
title: "Disabling All Cards Produces Empty State on Resources Page Without Network Errors"
priority: medium
type: functional
module: resources-configuration
status: ready
execution_type: manual
tags: [feat:settings, story:4772, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4772]
---
# ELITEA-0022: Disabling All Cards Produces Empty State on Resources Page Without Network Errors

**Module:** Resources Configuration · **Priority:** Medium · **Type:** Functional

**Objective:** Edge case: verify that disabling all 5 cards at once results in an appropriate empty state on the user-facing Resources page, without crashes, JavaScript errors, or network errors (no 4xx/5xx responses).

## Preconditions

Logged in as an ELITEA admin user.
All 5 cards are currently enabled.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Resources. | Resources configuration page is open. |
| 2 | Disable all 5 cards (Information, Documentation, Release Notes, Video Library, Tutorials) and save. | All toggles reflect disabled state and the configuration saves successfully. |
| 3 | Open the user-facing Resources page in any project. | The Resources page shows an empty state or an appropriate message. No cards are displayed. |
| 4 | Open the browser Network tab and check for errors on the Resources page. | No network errors (no 4xx or 5xx responses) are produced. |
| 5 | Return to Admin → Configuration → Resources and re-enable all cards. Save. | All cards are restored to enabled state. |

## Expected Final State

All cards are restored to enabled state.

## Pass/Fail Criteria

Pass: Resources page shows empty/placeholder state without errors; no network errors in browser console.
Fail: Page crashes, throws an error, or produces network errors when all cards are disabled.
