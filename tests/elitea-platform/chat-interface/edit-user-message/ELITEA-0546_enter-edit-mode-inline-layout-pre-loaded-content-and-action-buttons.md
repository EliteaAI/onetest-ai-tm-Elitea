---
id: ELITEA-0546
title: "Enter edit mode — inline layout, pre-loaded content, and action buttons"
priority: critical
type: functional
module: edit-user-message
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0546: Enter edit mode — inline layout, pre-loaded content, and action buttons

**Module:** Edit User Message · **Priority:** Critical · **Type:** Functional

**Objective:** Verify clicking Edit opens an inline editable field with original content and correct button placement.

**Coverage:**
- Inline editing (no modal/redirect)
- Content pre-loaded in editable field
- Cancel and Save and apply buttons visible at bottom-right

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A Chat Conversation with at least 1 completed user-assistant exchange

## Test Data

- Original last user message: "Explain the difference between REST and GraphQL"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a conversation where the last user message is "Explain the difference between REST and GraphQL". Click the Edit (pencil) icon on the last user message. | The message switches to inline editable mode. No modal opens. No page redirect occurs. URL remains the same. |
| 2 | Verify the content inside the editable field. | The editable field contains exactly "Explain the difference between REST and GraphQL" — the original message text is pre-loaded. |
| 3 | Verify the presence and position of action buttons. | "Cancel" and "Save and apply" buttons are both visible at the bottom-right of the editable message area. |

## Expected Final State

"Cancel" and "Save and apply" buttons are both visible at the bottom-right of the editable message area.

## Pass/Fail Criteria

**Pass:**
- Edit mode is inline within the chat area
- Original content is pre-loaded accurately
- Both buttons are visible at bottom-right

**Fail:**
- A modal or new page opens
- Editable field is empty or has incorrect content
- Buttons are missing or incorrectly positioned
