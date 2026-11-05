---
id: ELITEA-4463
title: "Schedules — waiting runs in pipelines: entry point, parallel branches, Test run and Run now, and no overlapping cron run"
priority: high
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:pipelines, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7304"]
---

# ELITEA-4463: Schedules — waiting runs in pipelines: entry point, parallel branches, Test run and Run now, and no overlapping cron run

**Module:** schedules · **Priority:** High · **Type:** Functional

**Objective:** Verify the #7304 waiting behaviour in pipelines and around the schedule: an **Entry point** pipeline waits and continues; a pause inside a **parallel branch** fails cleanly instead of hanging; **Test run** and **Run now** behave like a cron run; while a run waits, the next cron start makes no second run. Also record what happens when the schedule is paused or deleted while a run waits.

---

## Preconditions

- A team project **P**; the tester owns the schedules ("Pause and ask me").
- Pipeline **PL-E** (run mode **Entry point**) with a node using a toolkit that needs a sign-in (or a sensitive tool).
- Pipeline **PL-PAR** with a parallel step whose branch calls a listed sensitive tool.
- A cron of every 5 minutes on a schedule whose run pauses.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Test run PL-E's schedule. | **Waiting for approval** at the node. Approve (after sign-in, if needed) → the pipeline continues from that node and ends Success. |
| 2 | Test run PL-PAR's schedule. | The run ends **Failed** "a step inside a parallel branch needs an answer, and a scheduled run cannot give it". It does not stay in Running. |
| 3 | **Run now** a schedule whose run pauses. | Same waiting behaviour as a cron run; the run is the owner's own. |
| 4 | Let a 5-minute cron run pause and leave it waiting through two more cron times. | No second run is created and no second "needs approval" notice is sent. |
| 5 | Decide the waiting run. | The next cron time starts a new run normally. |
| 6 | Leave a run waiting for several hours (below the window), then Approve. | The run resumes (its checkpoint was kept). |
| 7 | **Record:** pause the schedule while a run waits; then delete a schedule while a run waits. | Note what happens to the waiting run (can it be decided? does it expire? does it disappear?). |
| 8 | **Record:** dry-run the risk check (form check before Save) and compare with Save for a missing credential under Pause and ask me. | The dry-run may list it as blocking while Save allows it (known gap). Note whether the UI shows the right result. |

---

## Expected Final State

No schedule had two active runs at the same time; no run stayed in Running after a parallel-branch pause.

---

## Pass/Fail Criteria

**Pass:**
- Steps 1–6 behave as above.

**Fail:**
- A parallel-branch pause leaves the run in Running, or a second cron run starts while one waits.
