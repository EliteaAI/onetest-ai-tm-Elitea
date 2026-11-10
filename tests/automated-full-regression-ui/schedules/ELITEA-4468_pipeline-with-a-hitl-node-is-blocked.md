---
id: ELITEA-4468
title: "Schedules — Pipeline With a HITL Node Is Blocked; Agent With a Missing Credential Waits Instead"
priority: high
type: regression
module: schedules
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:schedules, feat:pipelines, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7304"]
---

# ELITEA-4468: Schedules — Pipeline With a HITL Node Is Blocked; Agent With a Missing Credential Waits Instead

**Module:** schedules · **Priority:** high · **Type:** regression

**Objective:** Regression of the run statuses at start: a human step is **Blocked**, while a missing credential under Pause and ask me is **Waiting for approval** (not Blocked, since #7304). Manual source: ELITEA-4462.

---

## Preconditions

- **Test data:** import [`qa-sch-pipeline-human-steps.pipeline.md`](../../../test-data/schedules/qa-sch-pipeline-human-steps.pipeline.md), [`qa-sch-agent-artifact.agent.md`](../../../test-data/schedules/qa-sch-agent-artifact.agent.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- A pipeline with a **HITL** node (created by API) and a schedule for it.
- An agent with a missing credential and a "Pause and ask me" schedule (as in ELITEA-4465).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the pipeline's schedule review. | The human step is listed as blocking: 'Node "<id>" waits for a person'. |
| 2 | If the schedule can be saved, test run it. | Status **Blocked**; the run log has "Risk check: blocked: Node "<id>" waits for a person". |
| 3 | Test run the agent's schedule. | Status **Waiting for approval**, not Blocked. |
| 4 | Filter Run History by **Blocked**. | Only the pipeline run is listed. |

---

## Expected Final State

One Blocked run, one waiting run.

## Teardown

Reject the waiting run; delete the schedules, the pipeline and the agent.
