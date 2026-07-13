---
id: ELITEA-1873
title: "Discard changes resets all unsaved edits"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1873: Discard changes resets all unsaved edits

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking the Discard button (or confirming discard via a navigation dialog) reverts all unsaved changes to Name, Description, and Instructions back to their previously saved values.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent with saved Name, Description, and Instructions is available.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing agent's detail page and note current Name, Description, Instructions | Current saved values are noted |
| 2 | Modify all three fields to different values without saving | All three fields display new unsaved values |
| 3 | Click the Discard button (or navigate away and confirm discard in any dialog) | Discard action is triggered; any confirmation dialog is accepted |
| 4 | Verify all three fields have reverted to their previously saved values | Name, Description, and Instructions all match the originally noted saved values |

---

## Expected Final State

All three fields (Name, Description, Instructions) display the values that were saved prior to the unsaved edits. No unsaved modifications remain.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All three fields revert to their previously saved values after discard.

**Fail:**
- Any step produces an error or unexpected result.
- One or more fields retain the unsaved modified values after discard.
