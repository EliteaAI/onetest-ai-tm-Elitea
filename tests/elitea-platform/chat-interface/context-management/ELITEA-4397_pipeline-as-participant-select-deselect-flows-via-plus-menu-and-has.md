---
id: ELITEA-4397
title: "Pipeline-as-Participant Select/Deselect Flows via '+' Menu and '#' Mention Still Work Correctly"
priority: high
type: functional
module: context-management
status: draft
execution_type: manual
tags: [feat:chat, feat:context-management, feat:pipelines, issue:4840, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4840]
---
# ELITEA-4397: Pipeline-as-Participant Select/Deselect Flows via '+' Menu and '#' Mention Still Work Correctly

**Module:** Context Management · **Priority:** High · **Type:** Functional

**Objective:** Verify that adding, selecting, and deselecting a pipeline participant through both the "+" menu and the "#" mention flow continues to work correctly and keeps the PARTICIPANTS panel in sync, independent of its "messages" state configuration — as a UI-stability regression check alongside the issue #4840 counting-logic fix.

## Preconditions

- Logged in to {{base_url}}
- At least two pipelines are available to add as chat participants

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline 1 | Added/selected via "+" menu |
| Pipeline 2 | Selected inline via "#" mention |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a chat conversation, add a pipeline via the "+" menu and verify it appears in the PIPELINES section of PARTICIPANTS. | Pipeline 1 is added and correctly listed in the PIPELINES section of the PARTICIPANTS panel. |
| 2 | Select the pipeline, run it, then deselect it from the chat (without removing it from PARTICIPANTS). | Pipeline 1 selects, runs successfully, and deselects without error; it remains present in PARTICIPANTS. |
| 3 | Verify the PARTICIPANTS panel still correctly lists the pipeline after deselection. | PARTICIPANTS panel shows Pipeline 1 correctly, with no missing or stale entry. |
| 4 | Repeat using the "#" mention flow to select a different pipeline inline. | Pipeline 2 is selected inline via "#" mention without error and is reflected correctly in PARTICIPANTS. |
| 5 | Verify no duplicate entries, missing entries, or stale participant state occur after repeated select/deselect cycles. | After repeated select/deselect cycles via both flows, PARTICIPANTS panel shows no duplicates, no missing entries, and no stale/inconsistent state for either pipeline. |

## Expected Final State

Both the "+" menu and "#" mention flows for adding, selecting, and deselecting pipeline participants remain stable and correctly synchronized with the PARTICIPANTS panel, with no duplicate, missing, or stale entries, regardless of each pipeline's "messages" state configuration.

## Pass/Fail Criteria

**Pass:**
- Pipelines added via "+" menu and selected via "#" mention both behave correctly through select/deselect cycles.
- PARTICIPANTS panel remains accurate and in sync at every step, with no duplicate or stale entries.

**Fail:**
- PARTICIPANTS panel shows duplicate, missing, or stale pipeline entries after select/deselect cycles via either flow.
- Selecting/deselecting via "+" menu or "#" mention causes a UI error, crash, or broken participant state.
