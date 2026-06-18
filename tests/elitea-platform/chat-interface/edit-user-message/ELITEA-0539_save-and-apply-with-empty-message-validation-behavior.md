---
id: ELITEA-0539
title: "Save and apply with empty message — validation behavior"
priority: medium
type: functional
module: edit-user-message
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0539: Save and apply with empty message — validation behavior

**Module:** Edit User Message · **Priority:** Medium · **Type:** Functional

**Objective:** Verify system behavior when the user clears all text and attempts Save and apply.

**Coverage:**
- Empty message submission handling
- Validation error or graceful blocking

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A conversation with a last user message

## Test Data

- Original message: any non-empty text
- Action: clear all text leaving the field empty

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click Edit on the last user message. | Edit mode opens with content pre-loaded. |
| 2 | Clear all text from the editable field (field is now empty). | Field is empty. |
| 3 | Click "Save and apply". | Either: (a) The button is disabled/greyed when field is empty, OR (b) A validation message appears preventing submission, OR (c) The system handles empty submission gracefully without crashing. |

## Expected Final State

Either: (a) The button is disabled/greyed when field is empty, OR (b) A validation message appears preventing submission, OR (c) The system handles empty submission gracefully without crashing.

## Pass/Fail Criteria

**Pass:**
- System prevents empty submission with clear feedback, OR handles it gracefully without error
- No crash or unhandled exception
- User can continue using the conversation

**Fail:**
- Application crashes or shows unhandled error
- Empty message is submitted causing a broken conversation state
- User is stuck and cannot recover
