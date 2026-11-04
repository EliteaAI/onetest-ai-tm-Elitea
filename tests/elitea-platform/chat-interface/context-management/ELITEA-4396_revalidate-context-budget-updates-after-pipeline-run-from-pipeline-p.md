---
id: ELITEA-4396
title: "Re-validate: Context Budget Updates Correctly After Pipeline Run From the Pipeline Page (ELITEA-0526) and Does Not Reset When Run via Chat (ELITEA-0528)"
priority: high
type: regression
module: context-management
status: draft
execution_type: manual
tags: [feat:chat, feat:context-management, feat:pipelines, issue:4840, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4840]
---
# ELITEA-4396: Re-validate: Context Budget Updates Correctly After Pipeline Run From the Pipeline Page (ELITEA-0526) and Does Not Reset When Run via Chat (ELITEA-0528)

**Module:** Context Management · **Priority:** High · **Type:** Regression

**Objective:** Re-validate that the general pipeline-run counting behavior (outside the specific deselect scenario from issue #4840) remains correct on both the Pipeline page and in Chat, since both existing test cases exercise the same message-counting logic touched by the fix.

## Preconditions

- Logged in to {{base_url}}
- Existing test cases ELITEA-0526 and ELITEA-0528 setups are available
- A pipeline exists and is runnable both from the Pipeline page and as a chat participant

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline | Pipeline used for ELITEA-0526 / ELITEA-0528 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute ELITEA-0526: run a pipeline three times consecutively from the Pipeline page and confirm message/token counts increase monotonically after each run. | Message and token counts increase monotonically after each of the three consecutive runs — no decrease or reset. |
| 2 | Execute ELITEA-0528: send several normal chat messages, then run a pipeline participant in the same chat, and confirm the Context Budget reflects full history without resetting to a near-zero value. | After the pipeline runs within the chat, the Context Budget reflects the full prior conversation history plus the pipeline exchange — no reset to a near-zero/baseline value. |
| 3 | Record any deviation from previously passing baselines. | No deviation from the previously passing ELITEA-0526 and ELITEA-0528 baselines is observed. |

## Expected Final State

Context Budget counting behavior remains correct and monotonic for consecutive Pipeline-page runs (ELITEA-0526) and does not reset when a pipeline is run inside an active chat with prior history (ELITEA-0528), confirming no regression from the issue #4840 fix.

## Pass/Fail Criteria

**Pass:**
- Message/token counts increase monotonically across three consecutive Pipeline-page runs.
- Context Budget in Chat reflects full history (not a reset/near-zero value) after a pipeline run mid-conversation.
- No deviation from either previously passing baseline.

**Fail:**
- Message/token counts decrease or reset unexpectedly across consecutive Pipeline-page runs.
- Context Budget resets to a near-zero value after a pipeline runs mid-conversation in Chat.
- Either previously passing baseline (ELITEA-0526 or ELITEA-0528) now fails.
