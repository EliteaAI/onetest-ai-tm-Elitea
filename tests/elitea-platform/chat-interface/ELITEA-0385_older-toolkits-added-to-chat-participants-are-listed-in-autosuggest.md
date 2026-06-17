---
id: ELITEA-0385
title: "Older Toolkits Added to Chat Participants Are Listed in `/` Autosuggest"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: []
---
# ELITEA-0385: Older Toolkits Added to Chat Participants Are Listed in `/` Autosuggest

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the `/` autosuggest dropdown shows all Toolkits added to Conversation Participants — including ones that were created a long time ago (not at the top of the toolkits list sorted by creation date).

**Root Cause Context (bug #4839):** The autosuggest fetches participants sorted by `created_at DESC` in pages of 20. Toolkits created long ago appear on later pages that may never be fully loaded, making them silently absent from the dropdown.

**Coverage:**
- At least one recently created Toolkit and at least one old Toolkit are added to Conversation Participants
- Both appear in the `/` autosuggest dropdown
- Typing a partial name of the old Toolkit returns it — "No matching results" is NOT shown
- Results are complete and consistent

## Preconditions

- At least two Toolkits exist in the project: one created recently and one created a significant time ago (e.g., weeks or months earlier)
- Both Toolkits are added to the Conversation Participants panel in a Chat conversation
- The user is on the Chat page with the conversation ready

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Add both a recently created Toolkit and an older Toolkit (created weeks/months ago) to the Conversation Participants panel | Both Toolkits appear in the Participants panel |
| 2 | Click into the chat input field and type `/` | Autosuggest dropdown opens and lists both Toolkits — the old one and the new one are both visible |
| 3 | Type a partial name (first 3–4 characters) of the older Toolkit | The older Toolkit appears in the filtered autosuggest results — 'No matching results' is NOT shown |
| 4 | Clear the typed filter (backspace to just `/`) and type a partial name of the newer Toolkit | The newer Toolkit also appears correctly in filtered results |
| 5 | Select the older Toolkit from the autosuggest and send a message using it | The mention is inserted correctly and the message sends without errors — the older Toolkit responds as expected |

## Expected Final State

The mention is inserted correctly and the message sends without errors — the older Toolkit responds as expected

## Pass/Fail Criteria

PASS: Both old and new Toolkits are listed in autosuggest; older Toolkit found by partial-name filter; message via old Toolkit sends successfully
FAIL: Older Toolkit is absent from the dropdown; "No matching results" shown when filtering by old Toolkit name
