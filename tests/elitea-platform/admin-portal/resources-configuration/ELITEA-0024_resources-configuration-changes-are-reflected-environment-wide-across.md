---
id: ELITEA-0024
title: "Resources Configuration Changes Are Reflected Environment-wide Across All Projects"
priority: critical
type: functional
module: resources-configuration
status: ready
execution_type: manual
tags: [feat:settings, story:4772, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4772]
---
# ELITEA-0024: Resources Configuration Changes Are Reflected Environment-wide Across All Projects

**Module:** Resources Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that changes made in Admin → Configuration → Resources (card visibility) take effect across all projects in the environment without requiring per-project configuration. Covers AC6 of story EliteaAI/elitea_issues#4772.

## Preconditions

Logged in as an ELITEA admin user.
At least two different projects exist in the environment.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Resources. | Resources configuration page is open. |
| 2 | Disable any one card (e.g. Video Library) and save. | The change is saved successfully. |
| 3 | Open the Resources page in Project A. | The Video Library card is not visible. |
| 4 | Open the Resources page in Project B (a different project). | The Video Library card is also not visible in Project B, confirming environment-wide effect. |
| 5 | Re-enable the card in Admin → Configuration → Resources and save. | Change is saved. |
| 6 | Open the Resources page in Project A and Project B. | The card is visible again in both projects. |

## Expected Final State

The card is visible again in both projects.

## Pass/Fail Criteria

Pass: Card visibility change is reflected in Resources page for both projects without needing project-local config.
Fail: Change is only reflected in one project, or requires per-project action.
