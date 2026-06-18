---
id: ELITEA-1197
title: "Jira Toolkit — API Version Dropdown Exists, Defaults to Auto, and Persists All Three Values"
priority: high
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, int:jira, r-2.0.2]
requirements: []
---
# ELITEA-1197: Jira Toolkit — API Version Dropdown Exists, Defaults to Auto, and Persists All Three Values

**Module:** Jira Toolkit Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify that the API Version field in the Jira toolkit configuration is a dropdown (not a free-text input), has the correct options (Auto, V3, V2) with Auto as default, shows an ℹ️ tooltip, and that the selected value is saved and displayed correctly after saving.

**Coverage:**
- API Version field is a dropdown (not a text input)
- Default value is Auto
- All three options are selectable: Auto, V3, V2
- ℹ️ info icon is present next to the API Version label
- Selected value persists after saving and reloading the toolkit

## Preconditions

- Logged in to {{base_url}}
- A Jira toolkit exists (or can be created) in a Private or Team project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Jira toolkit configuration form. Locate the API Version field. | The API Version field is a **dropdown** control (not a free-text or numeric input). An ℹ️ icon is visible next to the label. |
| 2 | On a new Jira toolkit, check the default selected value of the API Version dropdown. | The API Version field defaults to **Auto**. |
| 3 | Click the API Version dropdown and inspect the available options. | The dropdown contains exactly three options: **Auto**, **V3**, **V2**. |
| 4 | Select **V3**, save the toolkit, and reopen it. | The API Version field shows **V3** after reopening — the value was persisted correctly. |
| 5 | Edit the toolkit, change API Version to **V2**, save, and reopen. | The API Version field shows **V2** after reopening — the value was persisted correctly. |
| 6 | Edit the toolkit, change API Version back to **Auto**, save, and reopen. | The API Version field shows **Auto** after reopening — the value was persisted correctly. |

## Expected Final State

The API Version field shows **Auto** after reopening — the value was persisted correctly.

## Pass/Fail Criteria

**Pass:**
- API Version is a dropdown (not a free-text/numeric input)
- Default value is Auto
- All three options (Auto, V3, V2) are present
- ℹ️ icon is visible next to the label
- Each selected value persists correctly after saving

**Fail:**
- API Version is still a free-text field
- Default is not Auto
- Any option is missing
- Selected value is not retained after saving
