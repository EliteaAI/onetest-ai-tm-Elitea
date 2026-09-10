---
id: ELITEA-3372
title: "Agent and Pipeline Builder work correctly when Skills Builder and Project Context Builder are enabled"
priority: critical
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, story:6239, regression, agent-pipeline-builder, ask-user, hitl]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3372: Agent and Pipeline Builder work correctly when Skills Builder and Project Context Builder are enabled

## Objective

Verify that enabling Skills Builder and Project Context Builder does not regress existing Agent & Pipeline Builder or Ask User flows, and sensitive tool HITL approval/rejection continues to work correctly.

## Preconditions

- User is logged in to `{{base_url}}`
- A project with an existing Agent and Pipeline exists
- A toolkit/tool requiring sensitive-action approval is configured and available

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Chat Modules menu | Menu opens |
| 2 | Enable Agent & Pipeline Builder, Ask User, Skills Builder, and Project Context Builder | All four modules show as enabled |
| 3 | Request creation of an Agent via chat with an incomplete description: "Create an agent for customer support" | The assistant proceeds with Agent creation and triggers an Ask User clarifying-question card |
| 4 | Answer the clarifying question(s) and submit | Agent creation flow resumes and completes successfully |
| 5 | Verify Agent chip appears in response | Agent chip/link is displayed |
| 6 | Repeat the same flow requesting Pipeline creation with incomplete info: "Create a pipeline for data processing" | Pipeline creation flow triggers Ask User clarification |
| 7 | Answer clarifying questions and submit | Pipeline creation completes successfully |
| 8 | Verify Pipeline chip appears in response | Pipeline chip/link is displayed |
| 9 | Trigger a sensitive tool call requiring approval in the same conversation | The existing approval prompt (HITL card) is shown |
| 10 | Approve the action | The action executes and the conversation continues normally |
| 11 | Trigger the sensitive tool call again | Approval prompt is shown again |
| 12 | Reject the action | The action is halted; conversation handles rejection gracefully |

## Expected Final State

Agent & Pipeline Builder, Ask User clarification, and HITL sensitive tool approval/rejection all continue to function exactly as before the Skills Builder / Project Context Builder modules were introduced.

## Pass/Fail Criteria

**Pass:**
- Agent creation via chat completes after clarification
- Pipeline creation via chat completes after clarification
- Ask User clarification triggers and resumes correctly
- HITL approval executes the action and continues conversation
- HITL rejection halts the action with existing handling
- No new errors or regressions observed

**Fail:**
- Agent or Pipeline creation fails, hangs, or behaves differently
- Ask User clarification does not trigger or does not resume
- HITL approval/rejection flow errors, hangs, or behaves differently
- Any regression in existing functionality when new modules are enabled
