---
id: ELITEA-1697
title: "Artifacts Tool Behavior Not Affected by Guardrails Changes"
priority: high
type: regression
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:artifacts, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1697: Artifacts Tool Behavior Not Affected by Guardrails Changes

**Module:** Admin Portal / Guardrails · **Priority:** High · **Type:** Regression

**Objective:** Verify that the Artifacts tool behavior is not impacted by the case-insensitive matching and live-reload changes to Guardrails.

## Preconditions

- Logged in as a user with access to Artifacts functionality
- Agent configured with Artifacts capability
- Guardrails configured with some blocked/sensitive tools (not Artifacts)

## Test Data

| Toolkit | Sensitive Tools (existing config) |
|---------|----------------------------------|
| `artifact` | `delete_file`, `append_data`, `create_new_bucket`, `edit_file`, `index_data`, `remove_index` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails page loads. Verify `artifact` toolkit has sensitive tools configured. |
| 2 | Open agent chat with Artifacts capability enabled. | Agent chat opens. |
| 3 | Trigger `delete_file` tool from artifact toolkit. | Authorization dialog appears before execution. |
| 4 | Authorize and verify execution. | Tool executes correctly after authorization. |
| 5 | Trigger `append_data` tool. | Authorization dialog appears. |
| 6 | Authorize and verify execution. | Tool executes correctly. |
| 7 | Trigger `edit_file` tool. | Authorization dialog appears. |
| 8 | Authorize and verify execution. | Tool executes correctly. |
| 9 | Trigger `create_new_bucket` tool. | Authorization dialog appears. |
| 10 | Trigger `index_data` tool. | Authorization dialog appears. |
| 11 | Trigger `remove_index` tool. | Authorization dialog appears. |
| 12 | Verify all artifact sensitive tools still require authorization after Guardrails live-reload changes. | All configured sensitive tools trigger authorization dialog as expected. |

## Expected Final State

Artifacts tool operates normally regardless of Guardrails configuration changes. The case-insensitive matching and live-reload changes have no impact on Artifacts functionality.

## Pass/Fail Criteria

**Pass:**
- `delete_file` triggers authorization dialog
- `append_data` triggers authorization dialog
- `create_new_bucket` triggers authorization dialog
- `edit_file` triggers authorization dialog
- `index_data` triggers authorization dialog
- `remove_index` triggers authorization dialog
- Tools execute correctly after authorization
- Sensitive tool behavior unchanged after Guardrails live-reload changes

**Fail:**
- Any artifact sensitive tool executes without authorization dialog
- Authorization dialog content changed unexpectedly
- Tool parameters not passed correctly after authorization
- Artifact tools inadvertently affected by case-insensitive matching changes
