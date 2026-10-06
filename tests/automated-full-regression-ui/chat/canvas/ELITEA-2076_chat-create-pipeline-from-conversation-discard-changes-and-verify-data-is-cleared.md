---
id: ELITEA-2076
title: "Chat – Create Pipeline from Conversation – Discard Changes and Verify Data is Cleared"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2076: Chat – Create Pipeline from Conversation – Discard Changes and Verify Data is Cleared

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that entering data in the Create New Pipeline canvas and clicking Discard clears all entered data without creating a pipeline.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Pipeline name | test-pipeline |
| Pipeline description | This is a test pipeline for validation |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to the Chats section and open or create a conversation | Conversation view is displayed |
| 2 | Click the + icon at the bottom left of the message input area | Popup menu opens |
| 3 | Click on "Pipelines" and then click "+ Create New Pipeline" | "Create New Pipeline" canvas opens on the right side |
| 4 | Verify the canvas header shows "Create New Pipeline" with X, "Discard", and "Save" buttons | Canvas header is correct |
| 5 | Type "test-pipeline" in the "Name *" field | Name appears in the field |
| 6 | Type "This is a test pipeline for validation" in the "Description *" field | Description appears in the field |
| 7 | Click the "Discard" button | Confirmation dialog appears asking to confirm discarding changes |
| 8 | Click "Discard" to confirm | Canvas content is cleared |
| 9 | Close the canvas by clicking "X" | Canvas closes |
| 10 | Verify no pipeline was created in the PARTICIPANTS panel | No pipeline appears in PARTICIPANTS |

---

## Expected Final State

All entered data is cleared after clicking Discard; no pipeline is created in the conversation.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Discard clears all entered data and no pipeline is created.

**Fail:**
- Any step produces an error or unexpected result.
- Pipeline is created despite discarding, or data is not cleared.
