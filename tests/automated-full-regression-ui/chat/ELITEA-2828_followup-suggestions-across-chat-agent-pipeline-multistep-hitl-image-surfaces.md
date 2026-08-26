---
id: ELITEA-2828
title: "Chat/Agents/Pipelines – Follow-Up Suggestions Behave Correctly Across Chat, Agent, and Pipeline Surfaces, Including Multi-Step, HITL, and Generated-Image Responses"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, feat:agents, feat:pipelines, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2828: Chat/Agents/Pipelines – Follow-Up Suggestions Behave Correctly Across Chat, Agent, and Pipeline Surfaces, Including Multi-Step, HITL, and Generated-Image Responses

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify follow-up suggestions surface correctly (only after the full/final turn) on the plain Chat page, the Agent page, and the Pipeline page — including single-step, multi-step agent/pipeline runs, a pipeline with a HITL node, and a response containing generated image(s) — and never appear mid-run on an intermediate step/stage/tool-call.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- Available: a plain Chat conversation; a single-step Agent; a single-step Pipeline; a multi-step Agent (multiple tool calls); a multi-step Pipeline (multiple stages); a Pipeline containing a HITL node; an Agent/Chat capable of generating an image in its response.

---

## Test Data

| Field | Value |
|-------|-------|
| Scenario 1 | Plain Chat page, regular conversation, no agent/pipeline |
| Scenario 2 | Agent page, single-step agent |
| Scenario 3 | Pipeline page, single-step pipeline |
| Scenario 4 | Multi-step agent (multiple tool calls before final answer) |
| Scenario 5 | Multi-step pipeline (multiple stages before final result) |
| Scenario 6 | Pipeline containing a HITL node |
| Scenario 7 | A response that includes one or more generated images |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Run Scenario 1 and send a suggestion-eligible message | Chips render after the response completes |
| 2 | Run Scenario 2 and send a suggestion-eligible message | Chips render after the agent's single-step response completes |
| 3 | Run Scenario 3 and trigger a suggestion-eligible pipeline run | Chips render after the single-step pipeline run completes |
| 4 | Run Scenario 4, observing intermediate tool-call/thinking steps | No chips render during intermediate steps; chips render only after the agent's full/final turn completes |
| 5 | Run Scenario 5, observing intermediate stages | No chips render during intermediate stages; chips render only after the pipeline's full run completes |
| 6 | Run Scenario 6 through to the HITL prompt, resolve it, and let the pipeline finish | No chips render while HITL is awaiting input; chips (if eligible) render only after the pipeline's final response following HITL resolution |
| 7 | Run Scenario 7 and wait for the image to fully render alongside any text | Suggestions render after the image is fully rendered, and the chip list does not overlap or interfere with the displayed image |

---

## Expected Final State

Across every surface and run shape tested, suggestion chips appear only once per fully-completed final turn, never on an intermediate step, and never conflict with rendered image content.

---

## Pass/Fail Criteria

**Pass:**
- All 7 scenarios show chips only after the final/full response, never during an intermediate step/stage/HITL wait.
- Image-inclusive responses render chips without overlapping the image.

**Fail:**
- Any scenario shows chips during an intermediate step, stage, or the HITL wait.
- Chips overlap or interfere with a generated image.
