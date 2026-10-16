---
id: ELITEA-3948
title: "Chat – Multiple consecutive conversations created from same folder"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6]
requirements: [EliteaAI/elitea_issues#1604]
---

# ELITEA-3948: Chat – Multiple consecutive conversations created from same folder

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that users can create multiple new conversations consecutively from the same folder via context menu without errors, and all conversations appear correctly in the folder.

---

## Preconditions

- User is logged in to `{{base_url}}`
- User is on the Chats section
- At least one folder exists in the Chats section

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Message 1 | First test conversation about AI |
| Message 2 | Second test conversation about ML |
| Message 3 | Third test conversation about NLP |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click three-dot icon (⋮) on the folder row → click "New chat" | First new conversation opens |
| 2 | Send message: "First test conversation about AI" and wait for auto-naming | First conversation is auto-named and appears in the folder |
| 3 | Click three-dot icon (⋮) on the same folder → click "New chat" | Second new conversation opens |
| 4 | Send message: "Second test conversation about ML" and wait for auto-naming | Second conversation is auto-named and appears in the folder |
| 5 | Click three-dot icon (⋮) on the same folder → click "New chat" | Third new conversation opens |
| 6 | Send message: "Third test conversation about NLP" and wait for auto-naming | Third conversation is auto-named and appears in the folder |
| 7 | Expand the folder and verify all three conversations are present | All three conversations are visible with correct names, no duplicates |
| 8 | Verify context menu and "New chat" option remain functional | Can still open context menu and create additional conversations |

---

## Expected Final State

- All three conversations are successfully created in the same folder
- Each conversation has a unique auto-generated name
- No duplicates, no UI freezing, context menu remains functional

---

## Pass/Fail Criteria

**Pass:**
- All three conversations are created successfully in the folder
- No duplicate entries exist
- No UI freezing or blocking occurs
- Context menu remains functional after multiple uses

**Fail:**
- Any conversation creation fails
- Duplicate conversations appear
- UI freezes or becomes unresponsive
- Context menu stops working
