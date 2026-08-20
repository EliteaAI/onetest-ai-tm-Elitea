---
id: ELITEA-2081
title: "Chat – Create Toolkit from Conversation – Close Canvas Without Saving and Verify No Toolkit Created"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_close_toolkit_canvas_without_saving.TestCloseToolkitCanvasWithoutSaving.test_close_toolkit_canvas_without_saving_creates_no_toolkit"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1615
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2081: Chat – Create Toolkit from Conversation – Close Canvas Without Saving and Verify No Toolkit Created

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that closing the toolkit canvas via the X button after discarding does not create a toolkit and no TOOLKITS section appears in the PARTICIPANTS panel.

---

## Preconditions

- User is logged in to the Elitea platform.
- The canvas has been cleared after discarding (following ELITEA-2080).

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Verify the canvas is still open and cleared after the previous discard | Canvas is open with empty fields |
| 2 | Click the X button in the top right corner to close the canvas | Canvas closes completely |
| 3 | Verify the conversation view is displayed | Conversation view is shown |
| 4 | Verify no new TOOLKITS section appears in the PARTICIPANTS panel | No toolkit was created |
| 5 | Verify no toolkit was created | PARTICIPANTS panel shows no toolkit entries |

---

## Expected Final State

The canvas is closed without saving and no toolkit is created or shown in the PARTICIPANTS panel.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No toolkit is created; PARTICIPANTS panel has no TOOLKITS section.

**Fail:**
- Any step produces an error or unexpected result.
- A toolkit appears in PARTICIPANTS despite not being saved.
