---
id: ELITEA-2484
title: "Toggle Context Management from OFF to ON applies personality"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-2484: Toggle Context Management from OFF to ON applies personality

**Module:** Settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify turning Context Management ON immediately applies personality

## Preconditions

- User in Chat, Context Management OFF, QA personality configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send message with Context Management OFF: "Hello" | |
| 2 | Observe neutral response | |
| 3 | Turn Context Management ON, select "QA" | |
| 4 | Send same message: "Hello" | |
| 5 | Observe QA personality response | |

## Expected Results

- First response is neutral
- Second response reflects QA personality
- Toggle immediately activates personality

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
