---
id: ELITEA-0461
title: "Verify Combined Error Message Display Under Toolkit Name"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [credential-validation, toolkit-management, participants-panel, health-indicator, ux-improvement, chat-ui, 3709]
requirements: [GitHub Issue #3709]
---
# ELITEA-0461: Verify Combined Error Message Display Under Toolkit Name

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the complete message "Misconfiguration errors found. Check the toolkit" is displayed under the toolkit name when health indicator appears, with "Check the toolkit" portion styled as an inline clickable link.

**Coverage:**
- Complete error message display
- Inline link styling within message
- Message placement under toolkit name
- Visual distinction of clickable link portion

## Preconditions

- User is logged in to ELITEA platform at {{base_url}}
- User has a conversation with a misconfigured toolkit participant
- Health indicator is visible next to the toolkit participant

## Test Data

- ELITEA URL: {{base_url}}
- Expected message text: "Misconfiguration errors found. Check the toolkit"
- Clickable portion: "Check the toolkit" (inline within the message)
- Expected styling: Underline, different color, or hover effect on "Check the toolkit"
- Message location: Directly under the toolkit participant name

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to a conversation with a misconfigured toolkit participant that displays the health indicator. | Conversation opens and yellow/orange health indicator is visible next to the toolkit participant. |
| 2 | Locate the area directly below the toolkit participant name. | The complete message 'Misconfiguration errors found. Check the toolkit' is displayed under the toolkit participant name. |
| 3 | Verify the message structure and identify the 'Check the toolkit' portion within the sentence. | The 'Check the toolkit' portion appears as part of the same sentence, styled differently to indicate it is clickable (underlined, different color, or other visual cue). |
| 4 | Verify the message positioning and formatting. | Complete message is clearly readable, properly formatted, positioned directly under the toolkit name, and the clickable link portion is visually distinguishable within the message. |

## Expected Final State

Complete message is clearly readable, properly formatted, positioned directly under the toolkit name, and the clickable link portion is visually distinguishable within the message.

## Pass/Fail Criteria

**Pass:**
- Complete message "Misconfiguration errors found. Check the toolkit" is displayed
- Message appears directly under the toolkit participant name
- "Check the toolkit" portion is visually distinguishable as a clickable link within the same sentence
- Message is clearly readable and properly formatted

**Fail:**
- Message is not displayed or partially displayed
- "Check the toolkit" appears as a separate element rather than inline within the message
- No visual indication that "Check the toolkit" is clickable
- Message appears in wrong location
- Message text is incorrect or incomplete
