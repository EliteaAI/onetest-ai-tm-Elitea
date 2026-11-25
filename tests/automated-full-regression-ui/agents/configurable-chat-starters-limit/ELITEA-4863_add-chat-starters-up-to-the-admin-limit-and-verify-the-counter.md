---
id: ELITEA-4863
title: "Add chat starters up to the admin limit and verify the counter and disabled add button"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7322]
---

# ELITEA-4863: Add chat starters up to the admin limit and verify the counter and disabled add button

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that the agent editor uses the admin limit for chat starters (M). The counter reads "n/M starters added." after every added starter, and the add button is disabled once the limit is reached. The test reads M and does not change it, so it runs against whatever value the host has.

---

## Preconditions

- User is logged in to `{{base_url}}` and has permission to create agents in the project.
- A platform admin token is available for the API read in step 1.
- No agent named "Regression Chat Starters Limit" exists in the project (delete it if it was left over from an earlier run).

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/agents/create` |
| Admin limit (API) | `GET {{base_url}}/api/v2/admin/plugin_config_values/administration/guardrails` → `values.max_conversation_starters` |
| Limit delivered to the editor (API) | `GET {{base_url}}/api/v2/elitea_core/platform_settings/prompt_lib` → `conversation_starters_max` |
| Name | Regression Chat Starters Limit |
| Description | Regression agent for the chat starter limit |
| Starter n (n = 1…M) | `Regression starter n` |
| Counter text | `n/M starters added.` |
| At-limit tooltip | `You have reached the limit of chat starters` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call the admin limit API from Test Data and note `max_conversation_starters` as M | 200; M is a whole number from 1 to 10 |
| 2 | Call the platform settings API from Test Data | 200; `conversation_starters_max` equals M |
| 3 | Open Agents and click + Agent | The new agent form opens |
| 4 | Enter the Name and Description from Test Data and scroll to the Conversation Starters section | The counter reads "0/M starters added."; the add button is enabled |
| 5 | Click the add button and type "Regression starter 1" | A starter field appears with the text; the counter reads "1/M starters added." |
| 6 | Repeat step 5 for n = 2 … M − 1 | After each added starter the counter reads "n/M starters added."; the add button stays enabled |
| 7 | Add starter M | The counter reads "M/M starters added."; the add button is disabled |
| 8 | Hover the disabled add button | The tooltip says "You have reached the limit of chat starters" |
| 9 | Try to click the disabled add button | No new starter field is added; the counter still reads "M/M starters added." |
| 10 | Leave the form without saving (Discard) | No agent named "Regression Chat Starters Limit" is created |

---

## Expected Final State

No test agent is left in the project. The admin limit is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- The editor's limit equals the admin value M
- The counter reads "n/M starters added." after every added starter, from 0 to M
- At M the add button is disabled, shows the at-limit tooltip, and adds nothing

**Fail:**
- The counter uses a different limit than M (for example a hardcoded 4), skips or lags a value, or doesn't update
- The add button is enabled at M, or is disabled before M
- More than M starter fields can be added

---

## Notes

- Selectors (`data-testid`) for automation: `agents-add-button`, `agent-name-input`, `agent-description-input`, `agent-conversation-starters-section`, `agent-conversation-starters-limit-counter`, `agent-conversation-starter-add`, `agent-conversation-starter-input` (nth n − 1).
- The tooltip on the disabled button is an MUI tooltip, so hover its wrapper element, not the button itself.
- The admin setting is shared by every user of the host, so this case only reads it. Cases that change the limit live in the manual suite.
- Manual source: ELITEA-4843, ELITEA-4844 (`tests/elitea-platform/agents/configurable-chat-starters-limit/`).
