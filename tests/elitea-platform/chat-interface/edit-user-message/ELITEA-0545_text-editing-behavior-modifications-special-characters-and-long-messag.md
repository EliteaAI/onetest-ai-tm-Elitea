---
id: ELITEA-0545
title: "Text editing behavior — modifications, special characters, and long messages"
priority: high
type: functional
module: edit-user-message
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0545: Text editing behavior — modifications, special characters, and long messages

**Module:** Edit User Message · **Priority:** High · **Type:** Functional

**Objective:** Verify the editable field supports full text editing including special characters and long content.

**Coverage:**
- Add, delete, rephrase text
- Special characters preserved (< > " emoji)
- Long messages (2000+ chars) handled without truncation

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A conversation with a last user message

## Test Data

- Original message: "Test message"
- Modified text with special chars: Compare <HTML> vs "JSX" & show emoji 🚀
- Long message: 2000+ character paragraph

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click Edit on the last user message. Modify text to: Compare <HTML> vs "JSX" & show emoji 🚀. | Text is editable. Special characters <, >, ", &, and emoji are entered and displayed correctly in the field. |
| 2 | Select a portion of the text and use Ctrl+C / Ctrl+V to copy/paste. | Copy/paste works as expected. |
| 3 | Clear the field and paste a 2000+ character paragraph. | The full content is displayed without truncation. No layout overflow or clipping occurs. |
| 4 | Click Cancel to exit edit mode. | Edit mode closes. Original message is restored unchanged. |

## Expected Final State

Edit mode closes. Original message is restored unchanged.

## Pass/Fail Criteria

**Pass:**
- All text modifications are accepted
- Special characters render correctly
- Long text is fully visible and editable
- Standard keyboard shortcuts work

**Fail:**
- Characters are escaped, stripped, or garbled
- Long message is truncated or causes layout break
- Copy/paste or cursor positioning fails
