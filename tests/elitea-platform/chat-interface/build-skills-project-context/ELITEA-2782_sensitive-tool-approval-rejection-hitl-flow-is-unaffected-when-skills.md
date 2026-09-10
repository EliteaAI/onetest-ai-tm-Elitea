---
id: ELITEA-2782
title: "Sensitive tool approval/rejection HITL flow is unaffected when Skills Builder and Project Context Builder are enabled"
priority: critical
type: regression
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, hitl, sensitive-tool-approval, regression]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2782: Sensitive tool approval/rejection HITL flow is unaffected when Skills Builder and Project Context Builder are enabled

## Preconditions

- User is logged in to `{{base_url}}`
- A toolkit/tool requiring sensitive-action approval is configured and available in the conversation

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enable Skills Builder and Project Context Builder alongside the sensitive-tool-requiring module | All three modules show as enabled |
| 2 | Trigger a sensitive tool call requiring approval in the same conversation | The existing approval prompt is shown as before |
| 3 | Approve the action | The action executes and the conversation continues normally |
| 4 | Trigger the sensitive tool call again and reject the action | The action is halted/handled exactly as it was before this feature was introduced |

## Expected Final State

Sensitive tool approval and rejection behave identically to pre-existing behavior with the new builder modules enabled.

## Pass/Fail Criteria

**Pass:**
- Approval executes the action and continues the conversation
- Rejection halts the action with existing handling, no regression

**Fail:**
- Approval/rejection flow errors, hangs, or behaves differently than before this feature was introduced
