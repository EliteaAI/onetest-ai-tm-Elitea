---
id: ELITEA-0865
title: "With interruption: adding interruption/HITL/printer resets trigger to Chat Message and shows warning"
priority: critical
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5085]
---
# ELITEA-0865: With interruption: adding interruption/HITL/printer resets trigger to Chat Message and shows warning

**Module:** Entrypoint Trigger Type · **Priority:** Critical · **Type:** Functional

**Objective:** Verify expected behavior for interactive pipeline elements: trigger resets to Chat Message and warning is shown.

**Coverage:**
- Add interruption between nodes
- Add HITL node
- Add printer node
- Exact warning text verification

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

Variant A: Add interruption between nodes
Variant B: Add HITL node
Variant C: Add printer node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open pipeline and set trigger to Schedule or Webhook. Save. | Trigger persists as selected. |
| 2 | Apply interactive change for each variant: add interruption, add HITL node, add printer node. Save after each. | Save succeeds for each variant. |
| 3 | Observe UI notification/warning after save. | Message shown: Trigger reset to Chat Message (pipeline now contains interactive elements). |
| 4 | Refresh and re-open pipeline settings for each variant. | Trigger is Chat Message and warning behavior matches expected design. |

## Expected Final State

Trigger is Chat Message and warning behavior matches expected design.

## Pass/Fail Criteria

Pass:
- Exact message shown: Trigger reset to Chat Message (pipeline now contains interactive elements)
- Trigger resets to Chat Message for interruption/HITL/printer scenarios

Fail:
- Warning missing or incorrect
- Trigger does not reset in interactive scenarios
- Reset happens without user-visible explanation
