---
id: ELITEA-1928
title: "Edit Remote MCP — Discard Changes"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: automated
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1928: Edit Remote MCP — Discard Changes

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that unsaved edits to a Remote MCP can be discarded using the Discard button, reverting all fields to their original values and resetting button states.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP is available and open on its detail page in Form view.

---

## Test Data

| Field | Value |
|-------|-------|
| Temporary Description | This should be discarded |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Remote MCP detail page in Form view | Detail page loads in Form view |
| 2 | Note current description value | Original description is observed |
| 3 | Change description to "This should be discarded" | Field displays the temporary value |
| 4 | Verify Save and Discard buttons become enabled | Both buttons are active |
| 5 | Click Discard | Discard action is triggered |
| 6 | Verify description reverts to original value | Description shows the original text |
| 7 | Verify Save and Discard buttons return to disabled state | Both buttons are disabled again |

---

## Expected Final State

All unsaved changes are discarded; the description field shows the original value and both action buttons are disabled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Description reverts to original and buttons return to disabled state after Discard.

**Fail:**
- Any step produces an error or unexpected result.
- Changes are not discarded or buttons remain enabled after Discard.
