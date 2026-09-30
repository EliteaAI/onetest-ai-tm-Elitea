---
id: ELITEA-3549
title: "& trigger shows only private participants (excludes public agents from Agent Hub)"
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
- A conversation is open in Chat
- The chat has 2 private agents added (user's own agents or team agents, added via # search)
- The chat has 1 public agent from Agent Hub added (added via # search)
- Chat message input field is visible and empty

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Private Agent 1 | "MyCodeHelper" (user's own agent) |
| Private Agent 2 | "TeamDataBot" (team agent) |
| Public Agent | "PublicAnalyzer" (from Agent Hub, public) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Verify participants panel shows all 3 agents | Participants panel lists: "MyCodeHelper", "TeamDataBot", "PublicAnalyzer" |
| 2 | Click the chat message input field | Input field is focused and empty |
| 3 | Type `&` | Private participant dropdown appears |
| 4 | Observe the dropdown list | Dropdown shows ONLY 2 private agents: "MyCodeHelper", "TeamDataBot" |
| 5 | Verify "PublicAnalyzer" is NOT shown | "PublicAnalyzer" (public agent from Agent Hub) is NOT in the dropdown |
| 6 | Press ESC to close dropdown | Dropdown closes |

## Expected Final State

The & dropdown shows only private participants (user's own agents, team agents), excluding public agents from Agent Hub that were added to the chat.

## Pass/Fail Criteria

**Pass:**
- & trigger opens private participant dropdown
- Dropdown shows only private agents (MyCodeHelper, TeamDataBot)
- Public agent from Agent Hub (PublicAnalyzer) is NOT shown
- Dropdown correctly filters by participant visibility

**Fail:**
- & dropdown shows public agents from Agent Hub
- & dropdown shows ALL agents (same as # search)
- Private agents are missing from & dropdown
- Dropdown does not appear on & keystroke
