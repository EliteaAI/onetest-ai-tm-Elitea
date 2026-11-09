---
id: ELITEA-4489
title: "Schedules — Create Validation and Risk Confirmation (API)"
priority: critical
type: regression
module: schedules
status: draft
execution_type: manual
tags: [automated:API:regression, feat:schedules, issue:7011, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7011"]
---

# ELITEA-4489: Schedules — Create Validation and Risk Confirmation (API)

**Module:** schedules · **Priority:** critical · **Type:** regression

**Objective:** Regression of the schedule create rules not covered by elitea-api-testing: minimum interval, cron, timezone, stop date, version ownership, and the risk confirmation with the fingerprint. Verified on stage2 on 2026-11-05. Manual source: ELITEA-4480.

---

## Preconditions

- An editor or admin JWT for a team project.
- Agent **A** (default version **VA**) with a toolkit that has a listed sensitive tool; agent **B** with version **VB**.
- Base body: `{name, entity_type: "agent", application_id: A, version_id: VA, prompt, cron: "0 3 1 1 *", timezone: "Asia/Yerevan", enabled: false, approval_rule: "pause_and_ask"}` sent to `POST /api/v2/elitea_core/schedules/prompt_lib/{project}`.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Base body with `cron: "* * * * *"`, then `"*/4 * * * *"`. | 400 `invalid_input`, field `cron`, "Runs must be at least 5 minutes apart". |
| 2 | `cron: "61 * * * *"`. | 400, field `cron`, "invalid cron expression: … out of range". |
| 3 | `timezone: "Mars/Base"`. | 400, field `timezone`, "timezone must be a valid IANA timezone name, …". |
| 4 | `version_id: VB`. | 400, field `version_id`, "The version does not belong to this agent or pipeline". |
| 5 | `expires_at: "2020-01-01T00:00:00Z"`. | 400, field `expires_at`, "The stop date is in the past". |
| 6 | Base body, no `risk_ack`. | 409 `risk_confirmation_required` with `sensitive` (the listed tools only) and a `fingerprint`. |
| 7 | `risk_ack: "<fingerprint>"` (a string). | 400, field `risk_ack`, "Input should be a valid dictionary or instance of RiskAck". |
| 8 | `risk_ack: {"fingerprint": "deadbeef"}`. | 409 `risk_changed`. |
| 9 | `risk_ack: {"fingerprint": "<fingerprint>"}`. | 201; `owner.id` = the caller; `approval_rule: pause_and_ask`; `warnings` list the sensitive tools; `next_run` = the cron time converted from Asia/Yerevan to UTC. |
| 10 | `POST …/check` with the same entity. | 200; same `sensitive` list and fingerprint; `blocking: []`. |

---

## Expected Final State

One schedule created in step 9.

## Teardown

`DELETE …/{schedule_id}` → 204; then `GET` → 404 "Schedule not found".
