---
id: ELITEA-4487
title: "Schedules — legacy pipeline schedules move to the new table once, keep running with the creator as owner, and the old trigger can't be set to Schedule"
priority: high
type: functional
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, feat:pipelines, feat:admin-platform, issue:7011, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011"]
---

# ELITEA-4487: Schedules — legacy pipeline schedules move to the new table once, keep running with the creator as owner, and the old trigger can't be set to Schedule

**Module:** schedules · **Priority:** High · **Type:** Functional

**Objective:** Verify REQ-30 / REQ-31: the admin task moves pipeline schedules stored in `pipeline_settings.trigger` into the Schedules table (with a dry run first), the creator becomes the owner, no schedule runs twice, and old versions stay readable. The legacy trigger API refuses new `schedule` writes and the pipeline Trigger selector shows a notice pointing to the Schedules page.

Related existing cases: ELITEA-2005 / ELITEA-2008 (Schedule removed from the entry-point Trigger select).

---

## Preconditions

- Admin Portal access (platform admin) to run admin tasks.
- On an environment before the migration (or a restored project): a pipeline version **PV** with a legacy schedule trigger (cron + timezone), created by user **UC**.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the migration admin task for the project with **dry run** on. | A report lists PV's schedule (cron, timezone, owner UC); nothing is written. |
| 2 | Run it without dry run. | PV's schedule appears on the Schedules page: owner **UC**, same cron and timezone, Active, entity = the pipeline, version = PV. |
| 3 | Run the task again. | No duplicate schedule. |
| 4 | Wait for the cron time. | **One** run (not two: the old trigger no longer fires). |
| 5 | Open PV in the pipeline editor → Trigger. | Schedule is not selectable; a notice points to the Schedules page; the old version opens read-only without errors. |
| 6 | API: `PUT …/pipeline_trigger/…/{version}/trigger` with `type: schedule`. | 400; the trigger stays unchanged. |
| 7 | Same API with `type: chat_message`, then `webhook`. | Saved as before. |
| 8 | **Record (rollback, only on a test env):** set `legacy_step_enabled=false` and run `schedules_restore_legacy_triggers`. | The legacy trigger is back on PV and the migrated schedule and its runs are removed. |

---

## Expected Final State

PV's schedule lives only in the Schedules table and runs once per cron time.

---

## Pass/Fail Criteria

**Pass:**
- Migration is idempotent, keeps the owner and timing, and nothing runs twice.

**Fail:**
- A duplicate schedule, a double run, a changed owner, or the legacy API still accepts `schedule`.
