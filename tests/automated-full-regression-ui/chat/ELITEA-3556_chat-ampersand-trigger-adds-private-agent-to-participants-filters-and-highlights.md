---
id: ELITEA-3556
title: "Chat – & trigger adds private agent to participants, filters list, and highlights already-added agents"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
automation_test_id: []
tags: [automated:UI:regression, feat:chat, feat:agents, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6368]
---

# ELITEA-3556: Chat – & trigger adds private agent to participants, filters list, and highlights already-added agents

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify the & (ampersand) trigger for private participants: opens dropdown with only private agents, filters in real-time, click adds agent to PARTICIPANTS (not to input), and already-added agents are highlighted in the dropdown.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has at least 2 private agents available: "Agent A", "Agent B"
- A conversation is open with NO agents in PARTICIPANTS panel initially

---

## Test Data

| Field | Value |
|-------|-------|
| Private Agent 1 | "Agent A" |
| Private Agent 2 | "Agent B" |
| Filter string | first letter of agent name |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a conversation; verify PARTICIPANTS panel has no AGENTS section | No AGENTS section visible |
| 2 | Type `&` in the message input field | Private participant dropdown appears showing available private agents |
| 3 | Type first letters to filter (e.g., "Ag") | Dropdown filters in real-time to show only matching agents |
| 4 | Click "Agent A" in the dropdown | Dropdown closes; Agent A is added to PARTICIPANTS panel; NO text is inserted into input field |
| 5 | Verify PARTICIPANTS panel shows AGENTS section with "Agent A" | Agent A listed in AGENTS section |
| 6 | Type `&` again in the message input | Dropdown appears; "Agent A" is visually highlighted/selected (already added) |
| 7 | Observe "Agent B" in dropdown | "Agent B" has normal styling (not highlighted, not yet added) |
| 8 | Click "Agent B" | Agent B is added to PARTICIPANTS; both agents now in AGENTS section |
| 9 | Type `&` again | Both "Agent A" and "Agent B" are highlighted in the dropdown |

---

## Expected Final State

Both agents are added to PARTICIPANTS panel via & trigger. The dropdown correctly shows only private agents, filters in real-time, and highlights agents that are already added to the conversation.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- & trigger shows only private agents (not public)
- Click on agent adds it to PARTICIPANTS (no text in input)
- Already-added agents are visually highlighted in dropdown
- Real-time filtering works

**Fail:**
- Any step produces an error or unexpected result.
- Agent is inserted as text instead of being added to PARTICIPANTS
- Public agents appear in & dropdown
- Already-added agents are not highlighted
