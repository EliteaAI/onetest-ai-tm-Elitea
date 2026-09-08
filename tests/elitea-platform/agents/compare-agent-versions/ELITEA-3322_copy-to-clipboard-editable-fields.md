---
id: ELITEA-3322
title: "Copy to clipboard works for all Agent editable text fields in version comparison"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 2+ versions containing Instructions, Welcome Message, and Chat Starters
- External text editor available for paste verification

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Instructions | "You are a helpful AI assistant for testing clipboard functionality." |
| Test Welcome Message | "Welcome! I'm here to help you test clipboard features." |
| Test Chat Starter | "How does the clipboard copy feature work?" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Agent | Modal opens successfully |
| 2 | Locate copy-to-clipboard button/icon for Instructions field in Version 1 column | Copy button/icon is visible near Instructions field |
| 3 | Click the copy button for Instructions | Success feedback appears (toast notification or checkmark icon) |
| 4 | Open external text editor and paste (Ctrl+V or Cmd+V) | Instructions text is pasted correctly: "You are a helpful AI assistant for testing clipboard functionality." |
| 5 | Navigate to User Interaction section | Section loads successfully |
| 6 | Locate copy button for Welcome Message field | Copy button is visible |
| 7 | Click copy button for Welcome Message | Success feedback appears |
| 8 | Paste into external editor | Welcome Message text pastes correctly |
| 9 | Locate copy button for Chat Starter text field | Copy button is visible |
| 10 | Click copy button for Chat Starter | Success feedback appears |
| 11 | Paste into external editor | Chat Starter text pastes correctly |
| 12 | Repeat Steps 2-11 for Version 2 column (right side) | All copy operations work for Version 2 fields as well |

## Expected Final State

Copy to clipboard functionality works for all editable text fields (Instructions, Welcome Message, Chat Starters) in both version columns with success feedback.

## Pass/Fail Criteria

**Pass:**
- Copy button visible and functional for all editable fields
- Success feedback displayed after copy action
- Correct content pasted into external editor
- Copy works for both version columns

**Fail:**
- Copy button missing or non-functional
- No success feedback after copy
- Incorrect content pasted
- Copy only works for one column
