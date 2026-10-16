---
id: ELITEA-3882
title: "Context Management ON - personality affects conversation"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:ai-personality, feat:context-management, feat:chat, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5392]
---
# ELITEA-3882: Context Management ON - personality affects conversation

**Module:** Settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify when Context Management is ON, personality type DOES affect conversation

## Preconditions

- User in new Chat conversation
- QA and Cynical personalities have distinct instructions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Context Management, turn ON | |
| 2 | Select "QA" personality | |
| 3 | Save and send message: "Explain unit testing" | |
| 4 | Observe technical, testing-focused response | |
| 5 | Change to "Cynical" personality in Context Management | |
| 6 | Send same message | |
| 7 | Observe skeptical, challenging response | |

## Expected Results

- Responses reflect selected personality when Context Management is ON
- QA response is technical and testing-focused
- Cynical response is skeptical and challenging

## Pass/Fail Criteria

**Pass:**
- All expected results are met
- No unexpected errors or warnings appear

**Fail:**
- Any expected result is not met
- Unexpected errors or failures occur
