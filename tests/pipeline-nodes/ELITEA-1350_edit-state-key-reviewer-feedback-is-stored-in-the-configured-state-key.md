---
id: ELITEA-1350
title: "EDIT STATE KEY: Reviewer Feedback Is Stored in the Configured State Key After Edit Action"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1350: EDIT STATE KEY: Reviewer Feedback Is Stored in the Configured State Key After Edit Action

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a reviewer clicks Edit and submits feedback text, the feedback is stored in the pipeline state under the configured EDIT STATE KEY.

**Coverage:**
- Edit action presents a feedback text input to the reviewer
- Submitted feedback is stored in the specified state key
- Downstream Edit route node can access the captured feedback value

## Preconditions

- Pipeline with HITL node; EDIT STATE KEY = reviewer_feedback
- Edit route connected to a downstream node that uses reviewer_feedback
- Pipeline runnable in Chat interface

## Test Data

Reviewer feedback text: Please revise section 2 for clarity.; EDIT STATE KEY: reviewer_feedback

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run the pipeline in Chat interface; wait for HITL pause | Pipeline pauses; USER MESSAGE shown; action buttons visible |
| 2 | Click Edit | An edit input area is presented for reviewer to type feedback |
| 3 | Enter 'Please revise section 2 for clarity.' in the edit field | Feedback text entered |
| 4 | Submit the edit feedback | Pipeline resumes via Edit route; no errors |
| 5 | Check Run Details or downstream node output for the reviewer_feedback key | reviewer_feedback = 'Please revise section 2 for clarity.' |

## Expected Final State

reviewer_feedback = 'Please revise section 2 for clarity.'

## Pass/Fail Criteria

**Pass:**
- EDIT STATE KEY contains the reviewer's exact feedback text after Edit submission
- Downstream node can access the feedback value

**Fail:**
- Feedback not stored in the state key
- Key is empty or contains a wrong value
- Edit route fails to execute
