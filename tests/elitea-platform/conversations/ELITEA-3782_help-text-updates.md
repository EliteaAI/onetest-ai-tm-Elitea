---
id: ELITEA-3782
title: "Verify Help Text Updates Based On Selection"
priority: medium
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, feat:chat, feat:export, ui, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3782: Verify Help Text Updates Based On Selection

**Module:** Conversations · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the help text below the radio buttons updates dynamically based on the selected export option.

**Coverage:**
- Help text displays correctly for "Without attachments" selection
- Help text updates when switching to "With attachments"
- Text change is immediate (no delay)
- Correct descriptive text for each option

## Preconditions

- Logged in to {{base_url}}
- Conversation exists with attachments
- User is the conversation creator

## Test Data

- Conversation with at least 1 attachment

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Right-click conversation with attachments | Context menu with "Export" |
| 2 | Click "Export" | Dialog opens |
| 3 | Verify "Without attachments" selected by default | Radio button selected |
| 4 | Read help text below radio buttons | Text reads: "Only chat messages will be exported as a JSON file." |
| 5 | Verify text is visible and readable | Text clearly displayed, adequate font size |
| 6 | Click "With attachments" radio button | Radio button becomes selected |
| 7 | Verify help text updates immediately | Text changes instantly (no delay) |
| 8 | Read updated help text | Text reads: "Chat messages and all attached and generated files/images will be exported as a ZIP archive." |
| 9 | Verify text clearly describes ZIP export | Mentions "ZIP archive" and "attached and generated files/images" |
| 10 | Click "Without attachments" again | Radio button selected |
| 11 | Verify help text reverts immediately | Text changes back to JSON description instantly |
| 12 | Read reverted help text | Text reads: "Only chat messages will be exported as a JSON file." |
| 13 | Alternate between options 2-3 more times | Help text updates correctly each time |
| 14 | Verify no lag or display issues | Updates smooth, no flickering or delay |

## Expected Final State

- Help text updates dynamically based on selection
- Correct descriptions for each option
- Updates are immediate
- No display issues

## Pass/Fail Criteria

**Pass:**
- Help text for "Without attachments": "Only chat messages will be exported as a JSON file."
- Help text for "With attachments": "Chat messages and all attached and generated files/images will be exported as a ZIP archive."
- Text updates immediately when selection changes
- No lag or display issues

**Fail:**
- Help text doesn't update or updates incorrectly
- Wrong descriptions for options
- Delay in text update
- Display issues (flickering, missing text)

## Postconditions

- Dialog remains functional
- Help text provides clear guidance to user
