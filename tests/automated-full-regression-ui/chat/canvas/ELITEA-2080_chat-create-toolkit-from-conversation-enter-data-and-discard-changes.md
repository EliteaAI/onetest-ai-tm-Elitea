---
id: ELITEA-2080
title: "Chat – Create Toolkit from Conversation – Enter Data and Discard Changes"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2080: Chat – Create Toolkit from Conversation – Enter Data and Discard Changes

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that entering data in the Create New Toolkit canvas and clicking Discard clears the entered data while keeping the canvas open.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit type | Artifact |
| Toolkit Name | test |
| Bucket | test |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats and open a conversation | Conversation view is displayed |
| 2 | Click the + icon and select "Toolkits" | Toolkits submenu opens |
| 3 | Click "+ Create New Toolkit" | "New Toolkit" canvas opens with "Choose the toolkit type" section |
| 4 | Type "Artifacts" in the search window and verify toolkits are filtered | Only Artifact-related toolkits are shown |
| 5 | Click on "Artifact" toolkit type | "New Artifact Toolkit" configuration canvas opens |
| 6 | Type "test" in the "Toolkit Name *" field | Name appears in the field |
| 7 | Type "test" in the "Bucket *" field | Bucket value appears in the field |
| 8 | Click the "Discard" button | Warning dialog appears asking "Are you sure you want to discard changes?" |
| 9 | Click "Discard" in the dialog to confirm | Canvas is cleared; entered data is removed |
| 10 | Verify the canvas remains open with empty/default fields | Canvas is open but cleared |

---

## Expected Final State

All entered data is cleared after confirming Discard; the canvas remains open showing empty or default fields.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Discard clears all entered data and canvas remains open.

**Fail:**
- Any step produces an error or unexpected result.
- Data is not cleared, or canvas closes unexpectedly.
