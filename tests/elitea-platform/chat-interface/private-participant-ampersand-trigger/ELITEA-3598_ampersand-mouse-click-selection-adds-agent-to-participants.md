---
id: ELITEA-3598
title: "& mouse click selection adds agent to participants"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, eng:frontend, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6368]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A conversation is open with NO agents in PARTICIPANTS panel
- Private agent "CodeHelper" exists in the project
- Chat message input field is visible and empty

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Private Agent | "CodeHelper" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click the chat message input field | Input field is focused and empty |
| 2 | Verify PARTICIPANTS panel shows no AGENTS section | No AGENTS section visible |
| 3 | Type `&` | Private participant dropdown appears showing "CodeHelper" |
| 4 | Click "CodeHelper" in the dropdown with the mouse | Dropdown closes |
| 5 | Observe the input field | Input field is empty (NO text inserted) |
| 6 | Observe the PARTICIPANTS panel | AGENTS section appears with "CodeHelper" listed |

## Expected Final State

Agent "CodeHelper" is added directly to the PARTICIPANTS panel. No text is inserted into the chat input field.

## Pass/Fail Criteria

**Pass:**
- Mouse click on dropdown item closes dropdown
- Agent is added to PARTICIPANTS panel (AGENTS section)
- NO text is inserted into the input field
- Agent is immediately available as a participant in the conversation

**Fail:**
- Click inserts text into the input field (like `&CodeHelper`)
- Dropdown stays open after click
- Agent is NOT added to PARTICIPANTS panel
