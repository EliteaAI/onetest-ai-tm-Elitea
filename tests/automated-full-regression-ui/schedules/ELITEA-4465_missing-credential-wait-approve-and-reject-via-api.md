---
id: ELITEA-4465
title: "Schedules — Credential Wait: Run Parks, Approve Refused While Missing, Approve After Adding Starts the Run, Reject Fails It"
priority: critical
type: regression
module: schedules
status: draft
execution_type: manual
tags: [automated:API:regression, feat:schedules, feat:credentials, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7304"]
---

# ELITEA-4465: Schedules — Credential Wait: Run Parks, Approve Refused While Missing, Approve After Adding Starts the Run, Reject Fails It

**Module:** schedules · **Priority:** critical · **Type:** regression

**Objective:** Regression of the missing-credential wait (#7304) through the API, with no external sign-in. Manual source: ELITEA-4459.

---

## Preconditions

- An agent with an **Artifact** toolkit that references a credential title that doesn't exist yet (all set up by API).
- A "Pause and ask me" schedule for the agent, owned by the test user.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start a **test run** of the schedule through the API. | The run status becomes `waiting_for_approval`; `conversation_id` is empty; the run events have a `paused` item with `need: credential` and the credential title. |
| 2 | `POST …/runs/{run}/decision` `{"action": "approve"}`. | 409, code `credential_missing`, "The credential is still missing. Add it, then approve again."; the run is still waiting. |
| 3 | Create the credential, then approve again. | 200; the run leaves the waiting state and ends `success`; the events have one `started` item. |
| 4 | Delete the credential, start another test run, then decide `{"action": "reject"}`. | The run ends `failed` with reason "rejected by the owner". |
| 5 | Decide the same run again. | 409 "This schedule run is not waiting for approval". |
| 6 | Decide with `{"action": "maybe"}` on a new waiting run. | 400. |

---

## Expected Final State

No run is left waiting.

## Teardown

Delete the schedule, the agent and the credential.
