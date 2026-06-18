---
id: ELITEA-0451
title: "Default Steps Limit Value is 25 for New Conversations"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3292]
---
# ELITEA-0451: Default Steps Limit Value is 25 for New Conversations

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the default Steps Limit value in the Model Settings modal for a newly created conversation is 25, ensuring backward compatibility is maintained.

**Coverage:**
- Default STEPS LIMIT value of 25 for brand-new conversations
- No user configuration required to maintain the previous default behavior

## Preconditions

- Logged in to {{base_url}}
- Private project selected
- Browser: Chrome (latest)

## Test Data

- Expected default STEPS LIMIT: 25

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat in the sidebar. Click '+ Create' to create a brand-new conversation. | An empty conversation is created and the chat input area is displayed. |
| 2 | Click the ⚙ (gear/settings) icon next to the model selector to open the Model Settings modal. | Model Settings modal opens. |
| 3 | Observe the value in the STEPS LIMIT field. | STEPS LIMIT field shows '25' as the default value. |

## Expected Final State

STEPS LIMIT field shows '25' as the default value.

## Pass/Fail Criteria

**Pass:**
- STEPS LIMIT field shows 25 in a newly created conversation without any prior configuration

**Fail:**
- STEPS LIMIT shows a value other than 25 (e.g. 0, empty, or any other number)
- STEPS LIMIT field is absent
