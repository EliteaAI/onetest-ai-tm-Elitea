---
id: ELITEA-0868
title: "Modifying name, fields, and structured output of the first entry node does not reset Schedule or Webhook trigger to Chat Message"
priority: critical
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5085]
---
# ELITEA-0868: Modifying name, fields, and structured output of the first entry node does not reset Schedule or Webhook trigger to Chat Message

**Module:** Entrypoint Trigger Type · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that editing the first entry node (name, fields, structured output) does not auto-switch trigger type to Chat Message when trigger is set to Schedule or Webhook.

**Coverage:**
- First entry node rename
- First entry node fields change
- First entry node structured output toggle
- Trigger persistence for Schedule and Webhook

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


Variant A: Trigger=Schedule; changes=name/fields/structured output
Variant B: Trigger=Webhook; changes=name/fields/structured output

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open pipeline and set trigger to Schedule. Save. | Trigger is saved as Schedule. |
| 2 | On the first entry node, change node name, update fields, and toggle structured output. Save. | Save succeeds without trigger reset warning. |
| 3 | Refresh the page and check trigger type. | Trigger remains Schedule and is not changed to Chat Message. |
| 4 | Set trigger to Webhook and save. | Trigger is saved as Webhook. |
| 5 | Repeat first entry node changes: name, fields, structured output. Save. | Save succeeds without trigger reset warning. |
| 6 | Refresh and check trigger type. | Trigger remains Webhook and is not changed to Chat Message. |

## Expected Final State

Trigger remains Webhook and is not changed to Chat Message.

## Pass/Fail Criteria

Pass:
- Schedule stays Schedule after changes
- Webhook stays Webhook after changes
- No auto-reset to Chat Message

Fail:
- Trigger changes to Chat Message
- Trigger value is lost after save/refresh
