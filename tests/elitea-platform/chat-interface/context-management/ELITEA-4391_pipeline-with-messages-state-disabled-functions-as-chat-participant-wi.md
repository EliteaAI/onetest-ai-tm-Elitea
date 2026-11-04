---
id: ELITEA-4391
title: "Pipeline With 'Messages' State Disabled Can Still Be Added, Selected, and Run as a Chat Participant Without Errors"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
tags: [feat:chat, feat:context-management, feat:pipelines, issue:4840, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4840]
---
# ELITEA-4391: Pipeline With 'Messages' State Disabled Can Still Be Added, Selected, and Run as a Chat Participant Without Errors

**Module:** Context Management · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a pipeline with the "messages" state disabled (if the toggle still exists post-fix) remains fully functional as a chat participant — no execution failure, no participant panel corruption, no chat crash.

## Preconditions

- Logged in to {{base_url}}
- A pipeline with "messages" state disabled exists and is available to add as a chat participant

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline | Pipeline with "messages" state disabled |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Chat conversation. | Chat conversation loads successfully. |
| 2 | Add the pipeline with "messages" state disabled as a participant via the "+" menu. | Pipeline is added without error. |
| 3 | Verify it appears correctly in the PARTICIPANTS panel (Pipelines section, correct name/icon). | Pipeline is listed with correct name, icon, and section placement; no corruption or duplicate entries. |
| 4 | Select the pipeline and send a message to trigger it. | Pipeline is selected without error. |
| 5 | Verify the pipeline executes and returns a response without error. | Pipeline runs to completion and returns a valid response in the chat. |
| 6 | Deselect the pipeline and send a follow-up normal message. | Deselection completes without error. |
| 7 | Verify the chat continues to function normally (no crash, no stuck "generating" state, no broken participant entry). | Chat remains fully functional: follow-up message sends and receives a response normally; PARTICIPANTS panel still shows the pipeline correctly; no stuck UI state. |

## Expected Final State

The pipeline with "messages" state disabled remains a fully functional, correctly displayed chat participant throughout add, select, run, and deselect actions, with the chat remaining stable and responsive afterward.

## Pass/Fail Criteria

**Pass:**
- Pipeline adds, selects, runs, and deselects without any error, crash, or stuck state.
- PARTICIPANTS panel displays the pipeline correctly at every stage.
- Chat remains functional for subsequent normal messages.

**Fail:**
- Pipeline fails to execute, chat crashes, or UI gets stuck in a "generating" state.
- PARTICIPANTS panel shows a corrupted, duplicated, or missing entry for the pipeline.
