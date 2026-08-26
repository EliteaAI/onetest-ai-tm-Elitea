---
id: ELITEA-2779
title: "Toolkit Configuration Form and Raw JSON View Toggle Functionality"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, smoke, configuration]
requirements: []
---
# ELITEA-2779: Toolkit Configuration Form and Raw JSON View Toggle Functionality

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional / Smoke

**Objective:** Verify that the Form view and Raw JSON view toggles work correctly on the Toolkit Details page, and that changes made in one view are reflected in the other.

**Coverage:**
- Form view displays editable fields correctly
- Raw JSON view displays configuration as valid JSON
- Toggle between views preserves unsaved changes
- Editing in Raw JSON reflects in Form view
- Editing in Form view reflects in Raw JSON view

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An existing toolkit with configurable parameters

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with multiple configuration fields |
| Test Value | "Test Description Update" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select an existing toolkit. | Toolkit details page opens in Form view (default). |
| 2 | Verify Form view is displayed with editable fields: Toolkit Name, Description, Credentials dropdown. | All fields are visible and editable. |
| 3 | Click "Show more" to expand additional configuration fields. | Additional configuration fields expand and become visible. |
| 4 | Modify the Description field to "Test Description Update". | Field value changes; unsaved changes indicator appears. |
| 5 | Click the "Raw JSON" toggle button. | View switches to Raw JSON editor showing the configuration as JSON. |
| 6 | Verify the modified Description appears in the JSON with the new value. | JSON contains the updated description value. |
| 7 | In Raw JSON view, change a different parameter value. | JSON is modified with the new value. |
| 8 | Click the "Form" toggle button to switch back. | View switches to Form view. |
| 9 | Verify the change made in Raw JSON is reflected in the Form view. | The corresponding field shows the updated value from the JSON edit. |

## Expected Final State

Both Form and Raw JSON views display synchronized configuration data, with all unsaved changes preserved across view toggles.

## Pass/Fail Criteria

**Pass:**
- Toggle between Form and Raw JSON works without data loss
- Changes in Form view appear in Raw JSON view
- Changes in Raw JSON view appear in Form view
- Raw JSON displays valid, parseable JSON

**Fail:**
- Data loss when toggling views
- Changes don't sync between views
- Raw JSON shows invalid or malformed JSON
- Toggle buttons don't respond
