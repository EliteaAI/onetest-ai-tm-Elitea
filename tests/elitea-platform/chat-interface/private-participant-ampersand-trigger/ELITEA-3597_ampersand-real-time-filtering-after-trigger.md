---
id: ELITEA-3597
title: "& real-time filtering after trigger with agent name characters"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, eng:frontend, nfr:usability, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6368]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A conversation is open with 3 private agents: "CodeHelper", "CodeReviewer", "DataProcessor"
- Chat message input field is visible and empty

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Private Agent 1 | "CodeHelper" |
| Private Agent 2 | "CodeReviewer" |
| Private Agent 3 | "DataProcessor" |
| Filter string | `cod` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click the chat message input field | Input field is focused and empty |
| 2 | Type `&` | Private participant dropdown appears showing all 3 agents |
| 3 | Type `c` (input is now `&c`) | Dropdown filters in real-time: "CodeHelper", "CodeReviewer" shown; "DataProcessor" hidden |
| 4 | Type `o` (input is now `&co`) | Dropdown shows "CodeHelper" and "CodeReviewer" |
| 5 | Type `d` (input is now `&cod`) | Dropdown shows "CodeHelper" and "CodeReviewer" (both contain "Cod") |
| 6 | Delete one character (Backspace, input is now `&co`) | Dropdown re-expands to show "CodeHelper" and "CodeReviewer" |
| 7 | Press ESC to close dropdown | Dropdown closes |

## Expected Final State

The & dropdown filters private participants in real-time as each character is typed, showing only agents whose names contain the typed substring (case-insensitive).

## Pass/Fail Criteria

**Pass:**
- Dropdown filters immediately after each keystroke
- Only private agents matching the substring are shown
- Deleting characters (Backspace) re-expands the filtered list
- Filter is case-insensitive

**Fail:**
- Dropdown does not filter in real-time
- All agents remain visible regardless of typed characters
- Filter does not update when characters are deleted
- Filter is case-sensitive
