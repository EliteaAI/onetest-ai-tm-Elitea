---
id: ELITEA-4395
title: "Re-validate: Pipeline 'Messages' State Accumulates Correctly Across Multiple Runs (ELITEA-0801)"
priority: high
type: regression
module: context-management
status: draft
execution_type: manual
tags: [feat:chat, feat:context-management, feat:pipelines, issue:4840, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4840]
---
# ELITEA-4395: Re-validate: Pipeline 'Messages' State Accumulates Correctly Across Multiple Runs (ELITEA-0801)

**Module:** Context Management · **Priority:** High · **Type:** Regression

**Objective:** Re-validate that the "messages" state still accumulates entries correctly across multiple pipeline runs, since the fix for issue #4840 modifies how the "messages" state is computed/tracked.

## Preconditions

- Logged in to {{base_url}}
- Existing test case ELITEA-0801 setup is available: a pipeline configured and runnable

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline | Pipeline used for ELITEA-0801 (with and without "messages" previously disabled, if still testable) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute ELITEA-0801 against the post-fix (R-2.0.8) build: run the pipeline twice and inspect the messages state after each run. | Run 1 completes successfully with an entry in the messages state; run 2 completes successfully with its own entry added. |
| 2 | Confirm entries from both runs are present after run 2 (prior history not discarded). | Messages state after run 2 contains entries from both run 1 and run 2 — no history loss. |
| 3 | Confirm behavior is consistent whether or not the pipeline previously had "messages" disabled (if still possible) and is now forced on. | Accumulation behavior is identical regardless of the pipeline's prior "messages" toggle state — no divergent behavior introduced by the fix. |

## Expected Final State

The pipeline's "messages" state continues to accumulate entries correctly across multiple runs post-fix, with no regression in history retention, regardless of the pipeline's prior "messages" toggle configuration.

## Pass/Fail Criteria

**Pass:**
- After run 2, messages state contains entries from both run 1 and run 2.
- Accumulation behavior is unaffected by whether the pipeline previously had "messages" disabled.

**Fail:**
- Messages state after run 2 contains only run 2 (prior history discarded).
- Messages state is empty after runs, or pipeline errors during execution.
- Accumulation behavior diverges based on the pipeline's prior "messages" toggle state.
