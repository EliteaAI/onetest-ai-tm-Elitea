---
id: ELITEA-4490
title: "Schedules — Pause, Resume and Edit Rules; Paused Schedule Has No Next Run (API)"
priority: high
type: regression
module: schedules
status: draft
execution_type: manual
tags: [automated:API:regression, feat:schedules, issue:7011, issue:7421, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011", "EliteaAI/elitea_issues#7421"]
---

# ELITEA-4490: Schedules — Pause, Resume and Edit Rules; Paused Schedule Has No Next Run (API)

**Module:** schedules · **Priority:** high · **Type:** regression

**Objective:** Regression of pause / resume and edit rules, including the #7421 fix (a paused schedule has no `next_run` and sorts with the paused ones). Expected to fail on step 3, 4 and 9 until #7421 is fixed (reproduced on stage2 2026-11-05 and 2026-11-09). Manual source: ELITEA-4484.

---

## Preconditions

- A schedule **S** owned by the caller (created as in ELITEA-4489), Active; other Active and paused schedules in the project.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | `POST …/S/pause`. | 200; `enabled: false`; `allowed_actions` has `resume`, not `pause`. |
| 2 | `POST …/S/pause` again. | 200 (no error). |
| 3 | `GET …/S`. | `next_run: null` (#7421). |
| 4 | `GET …?sort_by=next_run&sort_order=asc`. | S is listed with the other paused schedules, after all Active ones (#7421). |
| 5 | `PUT …/S` `{"enabled": true}`. | 400, field `enabled`, "enabled cannot be changed by an edit; use the pause or resume action of the schedule". |
| 6 | `PUT …/S` `{"cron": "*/2 * * * *"}`. | 400 "Runs must be at least 5 minutes apart". |
| 7 | `POST …/S/resume`. | 200; `enabled: true`; `next_run` = the next cron time after now. |
| 8 | `GET …?sort_by=bogus`. | 400 `invalid_input` "sort_by is not valid". |
| 9 | Create a schedule with `enabled: false`. | `next_run: null` (#7421). |

---

## Expected Final State

S is Active.

## Teardown

Delete S and the schedule from step 9.
