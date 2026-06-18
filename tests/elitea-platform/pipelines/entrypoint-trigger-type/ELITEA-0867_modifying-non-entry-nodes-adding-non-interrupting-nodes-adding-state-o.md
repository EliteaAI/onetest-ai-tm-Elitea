---
id: ELITEA-0867
title: "Modifying non-entry nodes, adding non-interrupting nodes, adding state, or changing entry point node does not reset Schedule/Webhook trigger"
priority: critical
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5085]
---
# ELITEA-0867: Modifying non-entry nodes, adding non-interrupting nodes, adding state, or changing entry point node does not reset Schedule/Webhook trigger

**Module:** Entrypoint Trigger Type · **Priority:** Critical · **Type:** Functional

**Objective:** Verify trigger type remains unchanged when editing non-entry nodes, adding non-interrupting nodes (LLM), adding state variables, and changing the entry point node.

**Coverage:**
- Non-entry node modifications
- New LLM node addition
- New pipeline state addition
- Entry point switched to another valid node
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

Variant A: Trigger=Schedule
Variant B: Trigger=Webhook
Change set: non-entry node edit + add LLM node + add state + switch entry point node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open pipeline and set trigger to Schedule. Save. | Trigger is saved as Schedule. |
| 2 | Modify a non-entry node and save. | Save succeeds; trigger unchanged. |
| 3 | Add a new LLM node (no interruption) and save. | Save succeeds; trigger unchanged. |
| 4 | Add a new state variable and save. | Save succeeds; trigger unchanged. |
| 5 | Change entry point to another valid node, save, and refresh. | Trigger remains Schedule; not changed to Chat Message. |
| 6 | Repeat steps 1-5 with trigger set to Webhook. | Trigger remains Webhook through all edits and refresh. |

## Expected Final State

Trigger remains Webhook through all edits and refresh.

## Pass/Fail Criteria

Pass:
- Schedule and Webhook are preserved across all covered changes
- No auto-reset to Chat Message

Fail:
- Trigger changes to Chat Message after any covered change
- Trigger value is lost after save/refresh
