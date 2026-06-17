---
id: ELITEA-0060
title: "Agent Saves Successfully With Valid Content in Welcome Message and Conversation Starter"
priority: critical
type: functional
module: agents
status: ready
execution_type: automated
tags: [meta:reported-by-support, nfr:validation, nfr:usability, eng:frontend, feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4963]
---
# ELITEA-0060: Agent Saves Successfully With Valid Content in Welcome Message and Conversation Starter

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the agent save workflow is not broken — an agent with content in both Welcome Message and Conversation Starters can be saved and the content persists.

**Coverage:**
- Save completes without error
- Field content persists on re-open

## Preconditions

- Logged in to {{base_url}}
- At least one existing agent open in edit mode in the Private project

## Test Data

- Welcome Message: 700-character string (e.g., "a" × 700) — under limit, valid
- Conversation Starter: 700-character string (e.g., "b" × 700) — under limit, valid

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an existing agent in edit mode; locate the Welcome Message field in the left configuration panel. | Agent configuration panel is open and editable. |
| 2 | Clear the Welcome Message field and enter the 700-character test string. | Text is entered. Character counter (collapsed mode) shows 68 characters remaining. |
| 3 | In Conversation Starters, click the '+' button and enter the 700-character test string for the new starter. | New starter entry is created with the entered text. Counter shows 68 remaining. |
| 4 | Click the Save button. | Save completes without an error toast or modal. |
| 5 | Close the agent and reopen it from the Agents list. | Welcome Message shows the 700-character text entered in step 2. Conversation Starter shows the 700-character text entered in step 3. |

## Expected Final State

Welcome Message shows the 700-character text entered in step 2. Conversation Starter shows the 700-character text entered in step 3.

## Pass/Fail Criteria

**Pass:**
- Save completes without errors
- Both field values persist correctly on re-open

**Fail:**
- Save fails or shows an error toast/modal
- Field content is lost or changed on re-open
