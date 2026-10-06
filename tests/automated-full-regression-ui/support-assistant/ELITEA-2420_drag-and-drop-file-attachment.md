---
id: ELITEA-2420
title: "Drag and drop file attachment"
priority: medium
type: functional
module: support-assistant
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-2420: Drag and drop file attachment

**Module:** support-assistant · **Priority:** medium · **Type:** functional

**Objective:** Verify that Drag and drop file attachment. Success is confirmed when click send — verify the message (with attachment) is submitted and the assistant acknowledges or processes it.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Support Assistant widget | Target page/section loads successfully. |
| 2 | Prepare a small test file (e.g., "drag-test.txt" with content "Drag and drop test") | Action completes without error and produces the expected UI state. |
| 3 | Drag the file from the file system and drop it onto the Support Assistant widget chat area | Action completes without error and produces the expected UI state. |
| 4 | Verify the file is accepted — a file preview or attachment chip appears in the input area | Condition holds as described. |
| 5 | Verify the Send button becomes enabled | Condition holds as described. |
| 6 | Click Send — verify the message (with attachment) is submitted and the assistant acknowledges or processes it | Control responds; expected next state is shown. |

---

## Expected Final State

Click Send — verify the message (with attachment) is submitted and the assistant acknowledges or processes it.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Drag and drop file attachment.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
