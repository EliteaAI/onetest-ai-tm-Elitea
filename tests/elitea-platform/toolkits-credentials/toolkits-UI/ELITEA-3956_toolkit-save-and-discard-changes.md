---
id: ELITEA-3956
title: "Toolkit Save and Discard Changes Functionality"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, smoke, save-discard]
requirements: []
---
# ELITEA-3956: Toolkit Save and Discard Changes Functionality

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional / Smoke

**Objective:** Verify that Save and Discard buttons function correctly on the Toolkit Details page, properly persisting or reverting changes.

**Coverage:**
- Save button persists changes to the backend
- Discard button reverts unsaved changes to last saved state
- Unsaved changes prompt appears when navigating away
- Save button is disabled when no changes exist

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An existing toolkit available for modification

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any existing toolkit |
| Original Description | (note the current value) |
| New Description | "Modified Description for Testing" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select an existing toolkit. | Toolkit details page opens. |
| 2 | Note the current Description value. | Current value recorded for verification. |
| 3 | Modify the Description field to "Modified Description for Testing". | Field updates; Save and Discard buttons become enabled/visible. |
| 4 | Click the "Discard" button. | Description reverts to the original value noted in step 2. |
| 5 | Modify the Description field again to "Modified Description for Testing". | Field updates; Save/Discard buttons enabled. |
| 6 | Click the "Save" button. | Changes are saved; success notification appears; Save/Discard buttons disable/hide. |
| 7 | Refresh the page (F5 or browser reload). | Page reloads with the saved value "Modified Description for Testing". |
| 8 | Modify the Description to a different value. | Unsaved changes state is active. |
| 9 | Without saving, click on a different section in the left sidebar (e.g., Agents). | Unsaved changes prompt/dialog appears asking to save or discard. |
| 10 | Click "Stay" or "Cancel" on the prompt. | Navigation is cancelled; user stays on Toolkit details page with unsaved changes. |

## Expected Final State

User remains on the Toolkit Details page with unsaved changes preserved after canceling navigation.

## Pass/Fail Criteria

**Pass:**
- Save persists changes to backend (verified by page refresh)
- Discard reverts to last saved state
- Unsaved changes prompt appears when navigating away
- Save/Discard buttons show correct enabled/disabled state

**Fail:**
- Save doesn't persist changes
- Discard doesn't revert changes
- No prompt when navigating away with unsaved changes
- Buttons always enabled or always disabled
