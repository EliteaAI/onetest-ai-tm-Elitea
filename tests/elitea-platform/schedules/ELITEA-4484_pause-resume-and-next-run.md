---
id: ELITEA-4484
title: "Schedules — pause and resume: no cron run while paused, Next run is cleared, Run Now still works"
priority: high
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, issue:7011, issue:7421, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011", "EliteaAI/elitea_issues#7421"]
---

# ELITEA-4484: Schedules — pause and resume: no cron run while paused, Next run is cleared, Run Now still works

**Module:** schedules · **Priority:** High · **Type:** Functional

**Objective:** Verify pausing and resuming a schedule (Schedules page row action, editor card toggle, API). A paused schedule starts no cron run, shows no Next run and sorts with the other paused schedules; resuming brings back the next cron time. Pause stops only the cron: Run Now still works.

**Known bug:** [#7421](https://github.com/EliteaAI/elitea_issues/issues/7421). Reproduced on stage2 by API: a paused schedule keeps `next_run` (also when created paused, and when auto-paused for `owner_lost_access`), and sorts by it.

---

## Preconditions

- **Test data:** import [`qa-sch-agent-basic.agent.md`](../../../test-data/schedules/qa-sch-agent-basic.agent.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- A schedule **S** with cron `*/5 * * * *`, Active, owned by the tester; other active and paused schedules in the project.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note S's Next run. Pause S on the Schedules page. | Status Paused. **Next run is empty.** (Known bug #7421: the old time stays.) |
| 2 | Pause S again (API `POST …/pause`). | No error; still paused. |
| 3 | Wait past two cron times. | No new run of S. |
| 4 | Sort the Schedules page by Next run. | S is with the other paused schedules, not among the active ones (#7421). |
| 5 | Run Now on paused S. | The run starts and is recorded as Manual; S stays paused. |
| 6 | Resume S. | Active; Next run = the next cron time after now (not a past time). |
| 7 | Wait for the next cron time. | A cron run starts (Trigger type Scheduled). |
| 8 | Create a new schedule already **paused** (or by API with `enabled: false`). | No Next run is shown. (Known bug #7421: a Next run is set at create.) |
| 9 | API edit with `"enabled": true`. | 400 "enabled cannot be changed by an edit; use the pause or resume action of the schedule". |

---

## Expected Final State

S is Active with a correct Next run.

---

## Pass/Fail Criteria

**Pass:**
- No cron run while paused; Next run cleared on pause and correct on resume.

**Fail:**
- A paused schedule runs on its cron.
- Steps 1, 4 or 8 show the old Next run (known bug #7421).
