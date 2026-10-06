---
id: ELITEA-2198
title: "Chat – Attachment Removal – Remove Individual Files by Clicking X Button"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2198: Chat – Attachment Removal – Remove Individual Files by Clicking X Button

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the X button on individual file chips removes them from the attachment area.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation with 4 files attached.

---

## Test Data

| Field | Value |
|-------|-------|
| Files attached | 4 test files |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Attach 4 files; verify all 4 chips shown | 4 chips visible |
| 2 | Click X on first file chip | First chip removed; 3 remain |
| 3 | Click X on another chip | That file removed; 2 remain |
| 4 | Verify remaining files still shown | 2 chips visible |

---

## Expected Final State

Individual file removal via X button works correctly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- X button removes individual file chips.

**Fail:**
- Any step produces an error or unexpected result.
- X button removes all files or doesn't work.
