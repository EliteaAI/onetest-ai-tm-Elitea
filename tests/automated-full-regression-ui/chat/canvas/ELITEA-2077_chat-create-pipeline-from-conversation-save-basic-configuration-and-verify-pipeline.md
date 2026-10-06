---
id: ELITEA-2077
title: "Chat – Create Pipeline from Conversation – Save Basic Configuration and Verify Pipeline is Created"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2077: Chat – Create Pipeline from Conversation – Save Basic Configuration and Verify Pipeline is Created

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that filling in the pipeline Name and Description and clicking Save creates the pipeline, transitions the canvas to edit mode with Configuration and Flow Editor tabs, and adds the pipeline chip to the message input area.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Pipeline name | test-pipeline |
| Pipeline description | A test pipeline for conversation |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats and open a conversation | Conversation view is displayed |
| 2 | Click + icon, select "Pipelines", click "+ Create New Pipeline" | "Create New Pipeline" canvas opens |
| 3 | Type "test-pipeline" in the "Name *" field | Name entered correctly |
| 4 | Type "A test pipeline for conversation" in the "Description *" field | Description entered correctly |
| 5 | Verify the ADVANCED section shows "Step limit" with value "25" and model chip | ADVANCED section is displayed correctly |
| 6 | Click the "Save" button | Pipeline is saved successfully |
| 7 | Verify the canvas header now shows "test-pipeline" with "base" version tag | Canvas transitions to edit mode |
| 8 | Verify two tabs appear at the top: "Configuration" (active) and "Flow Editor" | Both tabs visible; Configuration is active |
| 9 | Verify a pipeline chip appears in the message input area showing "test-pipeline", "base" version, and "Editing..." status | Pipeline chip is visible in message input |

---

## Expected Final State

The pipeline is created and saved; the canvas shows "Configuration" and "Flow Editor" tabs, and a pipeline chip with "Editing..." status appears in the message input area.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Pipeline is saved; canvas transitions to edit mode with both tabs; chip appears in message input.

**Fail:**
- Any step produces an error or unexpected result.
- Pipeline is not created, tabs are not shown, or chip is missing.
