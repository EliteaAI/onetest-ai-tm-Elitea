---
id: ELITEA-0029
title: "Card Enable/Disable State Persists After Save and Page Reload [Parametrized: Information, Documentation, Release Notes, Video Library, Tutorials]"
priority: high
type: functional
module: resources-configuration
status: ready
execution_type: manual
tags: [feat:settings, story:4772, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4772]
---
# ELITEA-0029: Card Enable/Disable State Persists After Save and Page Reload [Parametrized: Information, Documentation, Release Notes, Video Library, Tutorials]

**Module:** Resources Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify that the enabled/disabled toggle state of each card is persisted correctly after saving and reloading the Configuration → Resources page. Parametrized across all 5 cards. Covers AC3 persistence aspect of story EliteaAI/elitea_issues#4772.

## Preconditions

Logged in as an ELITEA admin user.
Parameters: run separately for each card — Information, Documentation, Release Notes, Video Library, Tutorials.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Resources. | Resources configuration page is open. |
| 2 | Toggle the target card to Disabled (if currently Enabled) or to Enabled (if currently Disabled). | The toggle reflects the new state. |
| 3 | Save the configuration. | Changes are saved successfully. |
| 4 | Reload the Configuration → Resources page. | Page reloads without error. |
| 5 | Inspect the toggle state for the same card. | The toggle shows the state that was saved — it has not reverted. |

## Expected Final State

The toggle shows the state that was saved — it has not reverted.

## Pass/Fail Criteria

Pass: Toggle state is retained after save and page reload.
Fail: State reverts to default or is not saved.
