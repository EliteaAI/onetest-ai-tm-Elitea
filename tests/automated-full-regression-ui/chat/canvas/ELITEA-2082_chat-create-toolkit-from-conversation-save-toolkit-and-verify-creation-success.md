---
id: ELITEA-2082
title: "Chat – Create Toolkit from Conversation – Save Toolkit and Verify Creation Success"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2082: Chat – Create Toolkit from Conversation – Save Toolkit and Verify Creation Success

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that filling in the toolkit Name and Bucket fields and clicking Save creates the toolkit successfully, showing a success notification and updating the canvas header.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit Name | test1 |
| Bucket | test1 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats and open a conversation | Conversation view is displayed |
| 2 | Click + icon, select "Toolkits", click "+ Create New Toolkit" | New Toolkit canvas opens |
| 3 | Select "Artifact" toolkit type | "New Artifact Toolkit" canvas opens |
| 4 | Type "test1" in "Toolkit Name *" field | Name entered correctly |
| 5 | Type "test1" in "Bucket *" field | Bucket entered correctly |
| 6 | Click the "Save" button | Success notification appears: "The toolkit has been created successfully" |
| 7 | Verify the canvas header now shows "test1" instead of "New Artifact Toolkit" | Canvas header updated to toolkit name |

---

## Expected Final State

The toolkit "test1" is created successfully; a green success notification appears and the canvas header updates to show the toolkit name.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Toolkit is created with success notification and canvas header updated.

**Fail:**
- Any step produces an error or unexpected result.
- Toolkit is not created, error notification appears, or canvas header is not updated.
