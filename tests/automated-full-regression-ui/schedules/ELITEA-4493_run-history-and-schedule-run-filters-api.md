---
id: ELITEA-4493
title: "Schedules — Run History and Schedule Run Filters Accept Valid Values and Reject Invalid Ones (API)"
priority: high
type: regression
module: schedules
status: draft
execution_type: manual
tags: [automated:API:regression, feat:schedules, issue:7338, issue:7435, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7338", "EliteaAI/elitea_issues#7435"]
---

# ELITEA-4493: Schedules — Run History and Schedule Run Filters Accept Valid Values and Reject Invalid Ones (API)

**Module:** schedules · **Priority:** high · **Type:** regression

**Objective:** Regression of the filters behind Run History and the Schedules page (#7338), verified on stage2 on 2026-11-05. The Schedules list accepts any `status` value (the UI only sends valid ones). Manual source: ELITEA-4483, ELITEA-4479.

---

## Preconditions

- **Test data:** import [`qa-sch-pipeline-basic.pipeline.md`](../../../test-data/schedules/qa-sch-pipeline-basic.pipeline.md) (see [test-data/schedules/README.md](../../../test-data/schedules/README.md) for the extra versions and environment setup).
- A pipeline **PL** with a schedule **S** that has manual and test runs, one Awaiting approval, of version **V**.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | `GET …/conversations/prompt_lib/{project}?source=pipeline&entity_name=application&entity_meta_id=PL&entity_meta_project_id={project}&trigger=manual` (then `cron`, `test`). | 200; only runs of that trigger. |
| 2 | Same with `status=waiting_for_approval`, `schedule_id=S`, `version_id=V`. | 200; matching rows only. |
| 3 | Same with `trigger=bogus`, `status=bogus`, `schedule_id=abc`. | 400 "trigger is not a valid value" / "status is not a valid value" / "schedule_id must be an integer". |
| 4 | `GET …/schedules/…/S/runs?status=bogus` and `?trigger=schedule_test`. | 400 listing the allowed values (`running, success, failed, skipped, blocked, waiting_for_approval` / `cron, manual, test`). |
| 5 | `GET …/schedules/prompt_lib/{project}?status=bogus`. | 200 with 0 rows (the list does not validate `status`; the UI offers only valid values — accepted). |
| 6 | `GET …/schedules/prompt_lib/{project}?status=running` while a run of S is active, and after a cron tick was skipped meanwhile. | S is listed (#7435; fix on main, not in 2.0.8). |

---

## Expected Final State

No data changed.

## Teardown

None.
