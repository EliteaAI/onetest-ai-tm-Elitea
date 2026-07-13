---
id: ELITEA-1888
title: "Save As Version creates a named version visible in version dropdown"
priority: high
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1888: Save As Version creates a named version visible in version dropdown

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that using "Save As Version" creates a new named version that is visible in the version dropdown and becomes the currently active version.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available in the "base" version.

---

## Test Data

| Field | Value |
|-------|-------|
| Version name | v2-test |
| Instruction change | Append a word to the existing Instructions field |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page in "base" version | The agent detail page loads with the base version active |
| 2 | Append a word to the Instructions field | The Instructions field is modified |
| 3 | Click "Save As Version" | A dialog appears asking for a version name |
| 4 | Verify a dialog appears asking for a version name | The version name input dialog is displayed |
| 5 | Enter "v2-test" and confirm | The dialog is submitted |
| 6 | Verify the version dropdown now lists at least "base" and "v2-test" | Both "base" and "v2-test" appear in the version dropdown |
| 7 | Verify "v2-test" is the currently active version | The version dropdown shows "v2-test" as the active/selected version |

---

## Expected Final State

The version dropdown lists at least "base" and "v2-test", with "v2-test" as the currently active version.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The new version "v2-test" appears in the dropdown and is set as the active version.

**Fail:**
- Any step produces an error or unexpected result.
- The new version does not appear in the dropdown, or is not set as the active version.
