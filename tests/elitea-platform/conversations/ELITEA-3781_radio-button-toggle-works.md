---
id: ELITEA-3781
title: "Verify Radio Button Toggle Between Without/With Attachments Works"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, feat:chat, feat:export, ui, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3781: Verify Radio Button Toggle Between Without/With Attachments Works

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that the radio button toggle between "Without attachments" and "With attachments" functions correctly with proper visual feedback.

**Coverage:**
- Both radio buttons visible
- Only one button selected at a time (mutual exclusivity)
- Visual feedback on selection
- Selection toggles correctly on click
- Selection state persists during dialog session

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
| 3 | Verify both radio buttons visible | "Without attachments" and "With attachments (N files · X MB)" both displayed |
| 4 | Verify default selection | One button is selected by default (likely "Without attachments") |
| 5 | Check visual indicator for selected button | Selected button shows filled circle or similar indicator |
| 6 | Check visual indicator for unselected button | Unselected button shows empty circle |
| 7 | Click "Without attachments" radio button (if not already selected) | Button becomes selected with visual feedback |
| 8 | Verify other option deselected | "With attachments" becomes deselected (empty circle) |
| 9 | Click "With attachments" radio button | Button becomes selected |
| 10 | Verify "Without attachments" deselected | "Without attachments" becomes deselected |
| 11 | Alternate clicking between options 3-4 times | Selection toggles correctly each time |
| 12 | Verify only one option selected at a time | Mutual exclusivity maintained throughout |
| 13 | Verify visual feedback immediate | No delay in selection change |
| 14 | Verify selection state persists | Selected option remains selected until changed |
| 15 | Test keyboard navigation (if supported) | Arrow keys or Space bar change selection |

## Expected Final State

- Radio buttons toggle correctly
- Only one option selected at any time
- Visual feedback clear and immediate
- Selection state maintained

## Pass/Fail Criteria

**Pass:**
- Both radio buttons visible and functional
- Only one option selected at a time (mutual exclusivity)
- Visual feedback clear (filled vs empty circle)
- Selection changes immediately on click
- Selection state persists during dialog session
- Keyboard navigation works (if supported)

**Fail:**
- Radio buttons not functional
- Both or neither option selected simultaneously
- No visual feedback on selection
- Selection doesn't change on click
- State not maintained

## Postconditions

- Dialog remains functional
- Selection affects export behavior (tested in other test cases)
