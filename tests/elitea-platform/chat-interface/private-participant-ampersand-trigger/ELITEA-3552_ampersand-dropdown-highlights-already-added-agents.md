---
id: ELITEA-3552
title: "& dropdown highlights already-added agents"
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
- A conversation is open with 2 agents already added to PARTICIPANTS: "Adviser", "Artifact"
- Private agent "bug 6595" exists but is NOT added to the conversation
- Chat message input field is visible and empty

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Already added agent 1 | "Adviser" |
| Already added agent 2 | "Artifact" |
| Not added agent | "bug 6595" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Verify PARTICIPANTS panel shows AGENTS section with "Adviser" and "Artifact" | Both agents listed in AGENTS section |
| 2 | Click the chat message input field | Input field is focused and empty |
| 3 | Type `&` | Private participant dropdown appears showing all available agents |
| 4 | Observe agents that are already in PARTICIPANTS ("Adviser", "Artifact") | Already-added agents are visually highlighted/selected (different styling) |
| 5 | Observe agent NOT in PARTICIPANTS ("bug 6595") | Not-added agent has normal styling (not highlighted) |
| 6 | Click "bug 6595" in the dropdown | Agent is added to PARTICIPANTS panel |
| 7 | Type `&` again | Dropdown shows all agents; now "bug 6595" is also highlighted along with "Adviser" and "Artifact" |

## Expected Final State

The & dropdown visually distinguishes agents already added to the conversation (highlighted) from agents not yet added (normal styling).

## Pass/Fail Criteria

**Pass:**
- Agents already in PARTICIPANTS are highlighted/selected in the dropdown
- Agents NOT in PARTICIPANTS have normal (non-highlighted) styling
- After adding a new agent, it becomes highlighted on next & trigger

**Fail:**
- All agents look the same regardless of participant status
- Highlighting does not update after adding an agent
- Dropdown fails to show distinction between added and not-added agents
