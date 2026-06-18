---
id: ELITEA-0805
title: "Nested Sub-Agent Pipeline Still Executes Correctly in Private Project"
priority: critical
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:pipelines, feat:agents, eng:backend, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4489]
---
# ELITEA-0805: Nested Sub-Agent Pipeline Still Executes Correctly in Private Project

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the fix does not regress nested sub-agent pipeline execution in Private projects, which was working correctly before the fix, covering both Chat and Agent page entry points.

**Coverage:**
- Agent page → Sub-Agent → Pipeline chain in a Private project (regression)
- Chat → Agent → Sub-Agent → Pipeline chain in a Private project (regression)
- No new errors introduced by the fix

## Preconditions

- Logged in to {{base_url}}
- Private project exists with identical agent structure: Parent Agent → Sub-Agent → Pipeline nested inside sub-agent

## Test Data

- Project type: Private
- Parent agent: `CreateABug` (or equivalent in Private project)
- Sub-agent: `EnhanceABug`
- Pipeline: `EnhanceABugPipeline`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Private project → Agents page. Open the parent agent and run it from the Agent page. | Sub-agent and pipeline execute. Full chain completes with valid output. No errors appear. |
| 2 | Navigate to the Private project → Chat. Create a new conversation. Add the parent agent as a participant. Send a prompt. | Chat → Agent → Sub-Agent → Pipeline chain completes. Valid response returned. No `checkpointer` error or any other new error appears. |

## Expected Final State

Chat → Agent → Sub-Agent → Pipeline chain completes. Valid response returned. No `checkpointer` error or any other new error appears.

## Pass/Fail Criteria

**Pass:**
- Both entry points (Agent page and Chat) complete without errors in the Private project
- Pipeline is triggered in both contexts
- No regressions to previously working behavior

**Fail:**
- Any error appears that was not present before the fix
- Pipeline fails to trigger in Private project after the fix is deployed
- Execution hangs or produces no output
