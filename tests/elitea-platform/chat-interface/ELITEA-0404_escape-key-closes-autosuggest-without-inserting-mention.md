---
id: ELITEA-0404
title: "Escape Key Closes `/` Autosuggest Without Inserting Mention"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0404: Escape Key Closes `/` Autosuggest Without Inserting Mention

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify Escape dismisses the autosuggest dropdown without inserting any mention, leaving the chat input in its typed state.

**Coverage:**
- Escape closes first autosuggest dropdown
- No mention inserted after Escape
- Input remains editable with typed text intact

## Preconditions

- Artifacts toolkit in Participants

## Test Data

- Input before Escape: /

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open chat with Artifacts in Participants. Type /. | Autosuggest dropdown appears. |
| 2 | Press Escape. | Dropdown closes. |
| 3 | Inspect the chat input. | Input contains / (typed text) but no mention highlight/chip. |
| 4 | Verify the input is still editable. | User can type additional characters. |

## Expected Final State

User can type additional characters.

## Pass/Fail Criteria

**Pass:**
- Dropdown closed by Escape
- No mention inserted

**Fail:**
- Dropdown not closed by Escape
- Mention inserted despite no selection
