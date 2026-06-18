---
id: ELITEA-0945
title: "Agent Ignore Project Context Toggle Blocks Injection from Agent Page and Chat"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, ignore-toggle, feat:settings, story:3395, r-2.0.4, agents, chat]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0945: Agent Ignore Project Context Toggle Blocks Injection from Agent Page and Chat

**Module:** Project Context · **Priority:** High · **Type:** Functional

**Objective:** Verify that the per-agent Ignore Project Context toggle correctly blocks injection for that specific agent when run from the Agent page and from a Chat page conversation.

**Coverage:**
- Agent with Ignore=OFF receives context from Agent page
- Agent with Ignore=ON does not receive context from Agent page
- Agent with Ignore=ON also does not receive context when added as Chat participant
- Other agents are unaffected
- Toggle persists and project-level toggle takes precedence

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Project Context phrase: `QA-TEST-PHRASE: Golden crane flies at noon`
- Two agents: Agent A (Ignore=OFF) and Agent B (Ignore=ON)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Project Context to 'QA-TEST-PHRASE: Golden crane flies at noon'. Enable toggle = ON. Save. | Content and toggle saved. |
| 2 | Open Agent A on the Agent page → Advanced. Confirm 'Ignore Project Context' is OFF by default. | Toggle is OFF. |
| 3 | Run Agent A from the Agent page. Ask: 'What is the QA-TEST-PHRASE?' | Agent A returns: 'Golden crane flies at noon'. |
| 4 | Open Agent B on the Agent page → Advanced. Set 'Ignore Project Context' = ON. Save. | Toggle saved as ON. |
| 5 | Run Agent B from the Agent page. Ask: 'What is the QA-TEST-PHRASE?' | Agent B does NOT return the phrase. |
| 6 | On the Chat page, start a new conversation and add Agent B as a participant. Ask the same question. | Agent B still does NOT return the phrase — the Ignore toggle applies in Chat too. |
| 7 | Run Agent A from the Agent page again. | Agent A still returns the phrase — Agent B's setting did not affect it. |
| 8 | Reload the page and check Agent B's toggle state. | Toggle is still ON (persisted). |
| 9 | Set project-level Enable toggle = OFF. Run Agent A from the Agent page. | Agent A does NOT return the phrase — project-level toggle overrides per-agent setting. |
| 10 | Set Enable toggle = ON again. Run Agent A. | Agent A returns the phrase again. |

## Expected Final State

Agent A returns the phrase again.

## Pass/Fail Criteria

**Pass:**
- Agent A (Ignore=OFF) returns phrase from Agent page
- Agent B (Ignore=ON) does not return phrase from Agent page
- Agent B does not return phrase when added to Chat
- Agent A still returns phrase after Agent B's toggle is set
- Project-level OFF overrides per-agent settings

**Fail:**
- Ignore=ON agent still returns phrase
- Setting Agent B's toggle affects Agent A
- Toggle does not persist after reload
