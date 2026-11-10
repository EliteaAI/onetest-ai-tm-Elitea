---
id: ELITEA-4485
title: "Schedules — cron runs start on time as the owner, an overlapping tick is Skipped, and the stop date ends the schedule"
priority: critical
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:agents, feat:pipelines, issue:7011, issue:7435, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011", "EliteaAI/elitea_issues#7435"]
---

# ELITEA-4485: Schedules — cron runs start on time as the owner, an overlapping tick is Skipped, and the stop date ends the schedule

**Module:** schedules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the scheduler tick: a due schedule starts once at its cron time (in its timezone), runs **as the schedule owner** with the prompt, and creates a "Scheduled run: <name>" chat with Trigger type Scheduled. While a run of the schedule is still active (Running or Awaiting approval), the next tick records a **Skipped** run ("the previous run is still running") and the schedule keeps its active status (#7435). A stop date ends the schedule.

---

## Preconditions

- **Test data:** import [`qa-sch-agent-artifact.agent.md`](../../../test-data/schedules/qa-sch-agent-artifact.agent.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- An agent **AG** with a working model and a toolkit with a listed sensitive tool (e.g. Artifact `list_indexes`).
- The tester owns the schedules. The project scheduler flags are on (Admin → Configuration → Runtime).

---

## Test Data

| Field | Value |
|-------|-------|
| Cron | `*/5 * * * *` |
| Timezone | a non-UTC zone, e.g. Asia/Yerevan |
| Prompt | "Call the list_indexes tool now, without asking anything." |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create an Active "Pause and ask me" schedule for AG with the test data. | Next run = the next 5-minute mark. |
| 2 | Wait for that time. | A run starts at that minute, Trigger type **Scheduled**. Run log: "Run started · trigger: cron", "Account: <owner> (schedule owner)". |
| 3 | Check the run. | It pauses before the sensitive tool: **Awaiting approval**. The schedule's last run status = Awaiting approval. |
| 4 | Wait for the next tick (5 min later) without deciding. | A **Skipped** run is added, reason "the previous run is still running". No second active run, no second approval notice. |
| 5 | Check the schedule's last run status and the Schedules page filter **Running** / **Awaiting approval**. | The schedule keeps **Awaiting approval** (the active run), not Skipped. **Known bug #7435 on 2.0.8** (reproduced on stage2 2026-11-09): the skipped tick changes the status to Skipped, the schedule leaves the Awaiting approval filter and shows under Skipped; fixed on main (elitea_core #683). |
| 5a | **Record:** after the run ends, check the schedule's Last run time. | It should be the real run's time, not the skipped tick's time (seen on stage2: the skipped tick's time stays). |
| 6 | Reject the waiting run. | Failed "rejected by the owner"; the next tick starts a new run normally. |
| 7 | Open the cron run's chat. | Named "Scheduled run: <schedule / agent>"; the prompt is the first message. |
| 8 | Pause the schedule. Set a **stop date** a few minutes ahead on another schedule and wait past it. | After the stop date no run starts; the schedule shows as ended / disabled with a reason. |
| 9 | Record the run times against the cron and the timezone. | Each run starts within the scheduled minute in the schedule's timezone. |

---

## Expected Final State

The schedules are paused or ended; one Skipped run per overlapping tick.

---

## Pass/Fail Criteria

**Pass:**
- Runs start on time as the owner; overlaps are Skipped and the schedule keeps its active status; the stop date stops it.

**Fail:**
- Two runs of one schedule are active at once; an overlap starts a second run; the active status is replaced by Skipped (known #7435 on 2.0.8).
