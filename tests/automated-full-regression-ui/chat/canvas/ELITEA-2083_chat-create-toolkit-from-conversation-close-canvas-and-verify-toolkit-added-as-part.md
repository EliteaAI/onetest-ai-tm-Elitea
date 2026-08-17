---
id: ELITEA-2083
title: "Chat – Create Toolkit from Conversation – Close Canvas and Verify Toolkit Added as Participant"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: tests.ui.chat.test_create_toolkit_from_conversation.TestCreateToolkitFromConversation.test_create_toolkit_from_conversation_close_canvas_and_verify_participant
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1576
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2083: Chat – Create Toolkit from Conversation – Close Canvas and Verify Toolkit Added as Participant

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that after saving toolkit "test1" and closing the canvas, the toolkit appears in the PARTICIPANTS panel under a TOOLKITS section.

---

## Preconditions

- User is logged in to the Elitea platform.
- Toolkit "test1" has been saved and the canvas is still open (following ELITEA-2082).

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit name | test1 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Verify the toolkit "test1" is saved and the canvas is open | Canvas shows "test1" in the header |
| 2 | Click the X button in the top right to close the canvas | Canvas closes completely |
| 3 | Observe the PARTICIPANTS panel on the right side | PARTICIPANTS panel is visible |
| 4 | Verify a "TOOLKITS" section is now present in the PARTICIPANTS panel | TOOLKITS section is displayed |
| 5 | Verify "test1" toolkit is listed under TOOLKITS section with a toolkit icon | Toolkit is listed with icon |

---

## Expected Final State

The toolkit "test1" is visible in the PARTICIPANTS panel under the TOOLKITS section after closing the canvas.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Toolkit is visible in PARTICIPANTS panel under TOOLKITS section.

**Fail:**
- Any step produces an error or unexpected result.
- Toolkit does not appear in PARTICIPANTS panel.
