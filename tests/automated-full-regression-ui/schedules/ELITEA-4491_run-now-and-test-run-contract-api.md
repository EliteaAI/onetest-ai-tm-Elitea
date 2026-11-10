---
id: ELITEA-4491
title: "Schedules — Run Now and Test Run Contract: Manual vs Test, One Active Run, Never Saved (API)"
priority: critical
type: regression
module: schedules
status: draft
execution_type: manual
tags: [automated:API:regression, feat:schedules, issue:7338, issue:7011, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7338", "EliteaAI/elitea_issues#7011"]
---

# ELITEA-4491: Schedules — Run Now and Test Run Contract: Manual vs Test, One Active Run, Never Saved (API)

**Module:** schedules · **Priority:** critical · **Type:** regression

**Objective:** Regression of the #7338 run contract, verified on stage2 on 2026-11-05: Run Now (`POST …/{id}/run`) and Test Run (`POST …/test_run`). Manual source: ELITEA-4482.

---

## Preconditions

- **Test data:** import [`qa-sch-agent-basic.agent.md`](../../../test-data/schedules/qa-sch-agent-basic.agent.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- A **paused** schedule **S** owned by the caller for agent **A** (working model).
- A second user who is project admin but not S's owner.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | `POST …/S/run` `{}`. | 400, field `trigger`, "Field required". |
| 2 | `POST …/S/run` `{"trigger": "cron"}`. | 400 "Input should be 'manual' or 'test'". |
| 3 | `POST …/S/run` `{"trigger": "manual"}` (S paused). | 202 `{run_id, application_id}`. |
| 4 | Same again while the run is active. | 409 `run_active`, "A run of this schedule is active", `active_run_id`. |
| 5 | After the run ends, `GET …/S`. | `last_run` and `last_run_status` updated; `next_run` unchanged; `enabled: false`. |
| 6 | `GET …/S/runs?trigger=manual`. | The run is listed with `trigger: manual`. |
| 7 | As the other admin, `POST …/S/run` `{"trigger": "manual"}`. | 403 `not_owner` "Only the owner of this schedule can run it". |
| 8 | `POST …/test_run` without `name`. | 400, field `name`, "Field required". |
| 9 | `POST …/test_run` with a full form for A. | 202 `{run_id, application_id}`. |
| 10 | `POST …/test_run` again while it is active. | 409 `run_active` "A test run of this schedule is active", `active_run_id`. |
| 11 | `GET …/test_run?application_id=A`. | The test run is listed, `trigger: test`, `schedule_id: null`. |
| 12 | `GET …?limit=50` (saved list). | No row for the test run. |
| 13 | `GET …/test_run/{another user's run}?application_id=A`. | 404 `run_not_found`. |
| 14 | `DELETE …/test_run`. | 405. |

---

## Expected Final State

S is paused with an unchanged `next_run`; no schedule was saved by the test run.

## Teardown

Delete S.
