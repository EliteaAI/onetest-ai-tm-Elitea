---
id: ELITEA-0863
title: "Pipeline Node Management"
priority: high
type: functional
module: pipelines
status: ready
execution_type: manual
tags: []
requirements: []
---
# ELITEA-0863: Pipeline Node Management

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can add LLM and Code nodes to pipelines, edit node properties, connect nodes, and delete nodes.

## Preconditions

- User logged into Elitea
- Test pipeline exists

## Test Data

- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Open pipeline editor | Canvas loads with Start/End nodes |
| ? | Click '+' button, add LLM node | LLM node appears on canvas |
| ? | Add Code node | Code node appears |
| ? | Connect LLM node to End | Edge drawn between nodes |
| ? | Edit node name | Name updated in canvas |

## Expected Final State

Name updated in canvas

## Pass/Fail Criteria

**Pass:**
- LLM node added successfully
- Code node added successfully
- Node name edits persist
- Nodes connect correctly
- Delete removes node

**Fail:**
- Node add fails
- Connections don't save
- Delete leaves orphan
