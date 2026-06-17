---
id: ELITEA-0402
title: "Non-Matching Text After `/` Shows Empty Autosuggest, No Error Message"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0402: Non-Matching Text After `/` Shows Empty Autosuggest, No Error Message

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that typing `/` followed by text that matches no participant Toolkit/MCP results in an empty autosuggest state with no error messages.

**Coverage:**
- Empty autosuggest when no match
- No error toast/banner shown
- Input remains editable

## Preconditions

- Artifacts toolkit in Participants

## Test Data

- Input: /xyz123nonexistent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open chat conversation with Artifacts in Participants. | Artifacts shown in Participants. |
| 2 | Click chat input and type /xyz123nonexistent. | Autosuggest dropdown opens with no matching items. |
| 3 | Verify the dropdown shows an empty state (no items). | No toolkit/MCP items listed. |
| 4 | Verify no error toast or inline error message appears. | No error indicators shown. |
| 5 | Delete the typed text and retype /A. | Autosuggest now shows Artifacts. |

## Expected Final State

Autosuggest now shows Artifacts.

## Pass/Fail Criteria

**Pass:**
- Empty dropdown for no-match input
- No error message shown
- Filtering recovers correctly when matching text is re-entered

**Fail:**
- Error message shown for non-matching input
- Dropdown does not update when text changes
