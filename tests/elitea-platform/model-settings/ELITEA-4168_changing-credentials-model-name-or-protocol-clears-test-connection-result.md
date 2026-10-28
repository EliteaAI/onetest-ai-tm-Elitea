---
id: ELITEA-4168
title: "Changing AI Credentials, Model Name, or API Protocol clears the previous Test connection result"
priority: high
type: functional
module: model-settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

## Preconditions

- User is logged in to `{{base_url}}` as a project admin.
- Valid non-DIAL credential/model and valid DIAL credential/model/protocol are available.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Non-DIAL combination | Any valid credential + model name |
| DIAL combination | Any valid credential + model name + protocol |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Test connection with non-DIAL credential/model | "Connected in N s" shown. |
| 2 | Change Model Name | Result disappears immediately. |
| 3 | Re-run test, then change AI Credentials | Result clears again. |
| 4 | With DIAL credential, run test, then change only API protocol | Result clears. |
| 5 | Observe result area after each clearing event | Stays cleared until Test connection is clicked again. |

## Expected Final State

Result clears on each of the three field changes and stays cleared until re-tested.

## Pass/Fail Criteria

**Pass:**
- Result clears for all three field changes and remains cleared.

**Fail:**
- A stale result remains visible after any of the three changes.
