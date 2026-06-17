---
id: ELITEA-0062
title: "Pasting Over-Limit Text — Text Truncated to 768 Chars With Visible Feedback"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [meta:reported-by-support, nfr:validation, nfr:usability, eng:frontend, feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4963]
---
# ELITEA-0062: Pasting Over-Limit Text — Text Truncated to 768 Chars With Visible Feedback

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that pasting text exceeding 768 characters into a field truncates the input to 768 characters and immediately shows the warning "0 characters left. You have reached the MAXIMUM character limit" — text overflow is never silently accepted.

**Coverage:**
- Pasted text truncated to exactly 768 characters for Welcome Message and Conversation Starter
- Counter immediately shows 0 in red after paste
- Warning "0 characters left. You have reached the MAXIMUM character limit" appears immediately after paste

## Preconditions

- Logged in to {{base_url}}
- Existing agent open in edit mode
- Full Screen editor open for Welcome Message or Conversation Starter field
- Field is empty

## Test Data

- Paste string: 1000-character string (e.g., "x" × 1000) — well above the 768-character limit

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Full Screen editor for the Welcome Message field. Clear all content. | Field is empty. Counter shows 768. |
| 2 | Paste the 1000-character string into the field. | Text is truncated to 768 characters (no more than 768 chars accepted). Counter shows 0 in red. |
| 3 | Verify the warning message is visible. | Warning reads exactly: '0 characters left. You have reached the MAXIMUM character limit'. |
| 4 | Verify the total character count in the field. | Field contains exactly 768 characters — excess characters beyond the limit are discarded. |
| 5 | Open a Conversation Starter entry's Full Screen editor. Clear content. Paste the 1000-character string. | Text is truncated to 768 characters. Counter shows 0 in red. Warning '0 characters left. You have reached the MAXIMUM character limit' is displayed. |
| 6 | Repeat steps 2-5 for collapsed mode for both fields (Welcome Message and Conversation Starter) | Text is truncated to 768 characters. Counter shows 0 in red. Warning '0 characters left. You have reached the MAXIMUM character limit' is displayed. |

## Expected Final State

Text is truncated to 768 characters. Counter shows 0 in red. Warning '0 characters left. You have reached the MAXIMUM character limit' is displayed.

## Pass/Fail Criteria

**Pass:**
- Pasted text is truncated to exactly 768 characters for both fields in Full Screen mode
- Counter immediately shows 0 in red after paste
- Warning "0 characters left. You have reached the MAXIMUM character limit" appears immediately

**Fail:**
- Text beyond 768 characters is accepted without truncation
- Counter does not update or stays default color after paste
- Warning message is missing or shows different text after paste
