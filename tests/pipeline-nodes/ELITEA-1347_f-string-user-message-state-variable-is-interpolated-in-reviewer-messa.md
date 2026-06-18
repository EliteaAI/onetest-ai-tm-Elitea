---
id: ELITEA-1347
title: "F-String USER MESSAGE: State Variable Is Interpolated in Reviewer Message"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1347: F-String USER MESSAGE: State Variable Is Interpolated in Reviewer Message

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that when USER MESSAGE type is F-String, pipeline state variables are correctly interpolated in the message shown to the reviewer.

**Coverage:**
- F-String template resolution at runtime
- Correct state value substitution in displayed message
- No raw template syntax visible to the reviewer

## Preconditions

- Pipeline with HITL node; USER MESSAGE type = F-String; value = 'Please review: {{state.input}}'
- Upstream node sets state.input to a known value
- Pipeline runnable in Chat interface

## Test Data

Pipeline input / state.input value: Test document; Expected USER MESSAGE output: Please review: Test document

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run the pipeline in Chat interface with input 'Test document' | Pipeline progresses; state.input = 'Test document' |
| 2 | Wait for HITL pause to activate | Pipeline pauses; USER MESSAGE is displayed |
| 3 | Read the displayed USER MESSAGE | Shows 'Please review: Test document' — F-String interpolated |
| 4 | Verify no raw template syntax is visible | No {{ or }} delimiters present in the displayed text |

## Expected Final State

No {{ or }} delimiters present in the displayed text

## Pass/Fail Criteria

**Pass:**
- F-String substitution occurs correctly
- Reviewer sees the resolved string with actual state values

**Fail:**
- Raw template syntax {{state.input}} appears in the reviewer message
- Wrong variable value substituted
