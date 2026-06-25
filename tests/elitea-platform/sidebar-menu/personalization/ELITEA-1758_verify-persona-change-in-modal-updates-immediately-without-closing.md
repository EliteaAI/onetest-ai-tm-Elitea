---
id: ELITEA-1758
title: "Verify persona change in modal updates immediately without closing"
priority: high
type: functional
module: ui
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, ui, real-time-update, modal]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1758: Verify persona change in modal updates immediately without closing

**Module:** UI · **Priority:** High · **Type:** Functional

**Objective:** Verify that persona changes in modal update immediately without requiring modal closure

## Preconditions

- User is logged into EliteA platform
- User has active conversation
- Context Management modal functional

## Test Data

- Personality sequence: Generic → Bare → Nerdy → Generic
- Custom instructions for Bare: "Be concise"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open existing conversation | Conversation displays |
| 2 | Open Context Management modal | Modal opens with current personality shown |
| 3 | Note current personality selection (e.g., Generic) | Current personality visible in dropdown |
| 4 | Click personality dropdown | Dropdown expands |
| 5 | Select "Bare" | Dropdown shows "Bare" selected |
| 6 | Verify custom instructions field appears immediately | Field visible without closing modal |
| 7 | Enter custom instructions: "Be concise" | Text entered |
| 8 | Keep modal open, click personality dropdown again | Dropdown expands |
| 9 | Select "Nerdy" | Dropdown shows "Nerdy" selected |
| 10 | Verify custom instructions field hides/becomes disabled immediately | Field no longer editable (Nerdy has fixed personality) |
| 11 | Keep modal open, select "Bare" again | Bare selected |
| 12 | Verify custom instructions field reappears with previous text | Field shows "Be concise" (preserved) |
| 13 | Change personality to "Generic" | Generic selected |
| 14 | Verify UI updates immediately | Custom instructions field hidden/disabled |
| 15 | Verify no page reload or modal close required | All changes instant while modal open |

## Expected Final State

- Personality changes update UI immediately within modal
- Custom instructions field shows/hides based on personality selection
- Previous custom instructions preserved when switching back to Bare
- No modal close or page reload required for updates
- Smooth, real-time UI updates

## Pass/Fail Criteria

**Pass:**
- Personality changes update immediately without closing modal
- Custom instructions field shows/hides instantly based on selection
- Previous custom instructions preserved correctly
- No delays, freezes, or need to close/reopen modal
- Smooth user experience

**Fail:**
- UI doesn't update until modal closed
- Custom instructions field doesn't show/hide correctly
- Previous custom instructions lost
- Delays or freezes during personality changes
- Need to close/reopen modal to see updates
