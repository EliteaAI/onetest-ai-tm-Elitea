---
id: ELITEA-4482
title: "Schedules — Run Now on a saved schedule vs Test Run on an unsaved form"
priority: critical
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:agents, issue:7338, issue:7011, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7338", "EliteaAI/elitea_issues#7011"]
---

# ELITEA-4482: Schedules — Run Now on a saved schedule vs Test Run on an unsaved form

**Module:** schedules · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the two run actions of #7338. **Run Now** runs the saved schedule, records it as **Manual**, always updates Last run and its status, never changes Next run, and can run a paused schedule. **Test Run** runs the current unsaved form, is marked **Test**, never saves or activates the schedule and never changes its Last / Next run. Only one run of each kind is active at a time.

---

## Preconditions

- **Test data:** import [`qa-sch-agent-basic.agent.md`](../../../test-data/schedules/qa-sch-agent-basic.agent.md), [`qa-sch-agent-artifact.agent.md`](../../../test-data/schedules/qa-sch-agent-artifact.agent.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- An agent **AG** whose model works, with no sensitive tool; a **paused** schedule **S** for AG owned by the tester.
- A second user who is not S's owner (project admin), for step 7.

---

## Steps

### Part A: Run Now

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open S. Note Next run. | The Runs header shows **Run Now** with the note "Runs the saved schedule and records it as Manual. Next run does not change." |
| 2 | Click **Run Now**. | A run starts although S is paused. The Runs (count) panel adds a card marked Manual. |
| 3 | Click Run Now again while it runs. | Refused: "A run is active" (409 `run_active`). |
| 4 | Wait for the end. | Last run and its status update (also for Failed / Awaiting approval). **Next run is unchanged.** S stays paused. |
| 5 | Open Run History for AG. | The run's **Trigger type** is **Manual**. |
| 6 | Open the run's chat. | Named "Manual run: <agent>". |
| 7 | As the other user (admin, not owner), open S. | **Run Now** is shown disabled with a hint, or refused with "Only the owner of this schedule can run it". |

### Part B: Test Run

| # | Action | Expected Result |
|---|--------|-----------------|
| 8 | Schedules → New schedule. Fill only part of the form. Click **Test Run**. | Refused with the missing required field (e.g. name). |
| 9 | Fill the form (do not save). Click **Test Run**. | A run starts; the Runs panel shows it marked **Test**. Nothing is saved: no new row on the Schedules page. |
| 10 | Click Test Run again while it runs. | Refused: one active test run per user and agent. |
| 11 | Change the prompt (still unsaved) and Test Run after the first ends. | The new run uses the changed prompt. |
| 12 | Save the form. | The action in the Runs header becomes **Run Now**. The saved schedule has no Last run from the test runs. |
| 13 | Run History for AG, filter **Trigger type = Test**. | The test runs are listed as Test. |
| 14 | Open a test run's chat. | Named "Manual run: <agent>" (a test run is a real run of the form, not a dry run; accepted). Only the Runs panel and Run History mark it **Test**. |
| 15 | Test Run an agent with a sensitive tool. | It always pauses for approval (a test run is never auto-approved) and is decided on the form's waiting card. |

---

## Expected Final State

S is still paused with an unchanged Next run; the new schedule is saved with no Last run from tests.

---

## Pass/Fail Criteria

**Pass:**
- Run Now and Test Run behave as above.

**Fail:**
- Run Now changes Next run or activates S; a Test Run saves or activates a schedule, or changes its Last run.

