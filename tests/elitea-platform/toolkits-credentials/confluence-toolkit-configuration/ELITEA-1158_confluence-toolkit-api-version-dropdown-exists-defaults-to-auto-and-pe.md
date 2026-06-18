---
id: ELITEA-1158
title: "Confluence Toolkit — API Version Dropdown Exists, Defaults to Auto, and Persists All Three Values"
priority: medium
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, r-2.0.2]
requirements: []
---
# ELITEA-1158: Confluence Toolkit — API Version Dropdown Exists, Defaults to Auto, and Persists All Three Values

**Module:** Confluence Toolkit Configuration · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the API Version dropdown field is present in the Confluence toolkit configuration form, has the correct options (Auto, V3, V2) with Auto as default, shows an ℹ️ tooltip, and that the selected value is saved and displayed correctly after saving.

**Coverage:**
- API Version dropdown field is present in Confluence toolkit form
- Default value is Auto
- All three options are selectable: Auto, V3, V2
- ℹ️ info icon is present next to the API Version label
- Selected value persists after saving and reloading the toolkit

**Note:** The API Version field is currently not used during Confluence tool calls — this test covers only the UI presence and value persistence.

## Preconditions

- Logged in to {{base_url}}
- A Confluence toolkit exists (or can be created) in a Private or Team project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Confluence toolkit configuration form. Locate the API Version field. | An **API Version** dropdown field is present in the form. An ℹ️ icon is visible next to the label. |
| 2 | On a new Confluence toolkit, check the default selected value of the API Version dropdown. | The API Version field defaults to **Auto**. |
| 3 | Click the API Version dropdown and inspect the available options. | The dropdown contains exactly three options: **Auto**, **V3**, **V2**. |
| 4 | Select **V3**, save the toolkit, and reopen it. | The API Version field shows **V3** after reopening — the value was persisted correctly. |
| 5 | Select **V2**, save the toolkit, and reopen it. | The API Version field shows **V2** after reopening — the value was persisted correctly. |
| 6 | Select **Auto**, save the toolkit, and reopen it. | The API Version field shows **Auto** after reopening — the value was persisted correctly. |

## Expected Final State

The API Version field shows **Auto** after reopening — the value was persisted correctly.

## Pass/Fail Criteria

**Pass:**
- API Version dropdown is present in the Confluence toolkit form
- Default value is Auto
- All three options (Auto, V3, V2) are present
- ℹ️ icon is visible next to the label
- Each selected value persists correctly after saving

**Fail:**
- API Version field is absent from the Confluence toolkit form
- Default is not Auto
- Any option is missing
- Selected value is not retained after saving
