---
id: ELITEA-0866
title: "When Chat Message trigger is selected, pipeline changes do not switch trigger to another type"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5085]
---
# ELITEA-0866: When Chat Message trigger is selected, pipeline changes do not switch trigger to another type

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verify that when Chat Message is selected as trigger, allowed pipeline modifications do not switch trigger to Schedule or Webhook.

**Coverage:**
- Entry node updates
- Non-entry node updates
- New non-interrupting node addition
- State addition
- Entry point node switch

## Preconditions

Logged into ELITEA stage/dev with pipeline edit permissions

## Test Data

Starting pipeline YAML:

```yaml

state:
  funny_joke:
    type: str
    value: ''
  input:
    type: str
  joke:
    type: str
    value: ''
  messages:
    type: list
entry_point: comedian
nodes:
  - id: comedian
    type: llm
    input: []
    input_mapping:
      chat_history:
        type: variable
        value: messages
      system:
        type: fixed
        value: You're the funniest comedian, you will be telling some random joke to user
      task:
        type: fixed
        value: tell a joke
    output:
      - joke
    structured_output: false
    transition: improve_joke
  - id: improve_joke
    type: llm
    input:
      - joke
    input_mapping:
      chat_history:
        type: variable
        value: messages
      system:
        type: fixed
        value: You're the funniest comedian, you will be given a joke, you have to make it funnier without asking any questions or anything. Just it make funnier
      task:
        type: fstring
        value: 'Joke: {joke}'
    output:
      - funny_joke
    structured_output: false
    transition: END

```

Trigger type: Chat Message
Changes: entry/non-entry edits, add LLM node, add state, switch entry point

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open pipeline, set trigger to Chat Message, and save. | Trigger is saved as Chat Message. |
| 2 | Perform changes: entry node edit, non-entry node edit, add LLM node, add state variable, switch entry point node. Save after each. | All saves succeed. |
| 3 | Refresh page after final save and check trigger. | Trigger remains Chat Message. |
| 4 | Re-open pipeline settings and verify trigger value. | Trigger is still Chat Message and not switched to another type. |

## Expected Final State

Trigger is still Chat Message and not switched to another type.

## Pass/Fail Criteria

Pass:
- Chat Message remains selected through all covered changes
- No switch to Schedule or Webhook

Fail:
- Trigger changes from Chat Message after any edit or refresh
