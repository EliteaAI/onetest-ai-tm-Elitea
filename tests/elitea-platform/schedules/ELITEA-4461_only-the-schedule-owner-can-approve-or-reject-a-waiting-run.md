---
id: ELITEA-4461
title: "Schedules — only the schedule owner can approve or reject a waiting run, from the UI, the chat and the decision API"
priority: critical
type: security
module: schedules
status: ready
execution_type: manual
tags: [feat:schedules, nfr:security, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7304"]
---

# ELITEA-4461: Schedules — only the schedule owner can approve or reject a waiting run, from the UI, the chat and the decision API

**Module:** schedules · **Priority:** Critical · **Type:** Security

**Objective:** Verify that only the **owner** of a schedule decides its waiting runs (#7304). A project admin, editor or viewer can't approve or reject, in the UI, in the run's chat, or through `POST …/schedules/{mode}/{project}/{schedule}/runs/{run}/decision`. Check the decision API's other refusals.

---

## Preconditions

- A team project **P** with the owner **OW** (editor or admin), a project admin **ADM**, an editor **ED** and a viewer **VW**.
- OW's "Pause and ask me" schedules: **S1** whose run waits for a **missing credential** (no chat), **S2** whose run waits for a **sensitive tool** (with chat).
- Keycloak JWTs for each user.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ADM, open S1's waiting run. | Approve / Reject are not available (or disabled). |
| 2 | As ADM, `POST …/runs/{run}/decision` `{"action": "approve"}` for S1's run. | 403 "Only the schedule owner can approve or reject this run". The run keeps waiting. |
| 3 | As ADM, open S2's run chat and try to approve the pause. | Refused; the run keeps waiting. |
| 4 | Repeat steps 1–3 as ED and as VW. | Refused (403) every time. |
| 5 | As OW, decision API with `{"action": "maybe"}`. | 400. |
| 6 | As OW, decision API for S2's run (it has a chat). | 409 "Decide this run in its chat". |
| 7 | As OW, approve S1's run with the credential added, then send the same approve again. | First: the run starts. Second: 409 "This schedule run is not waiting for approval". |
| 8 | As OW, open S2's waiting run in **two tabs**; Approve in one, Reject in the other. | Only one decision applies; the other is refused or has no effect. |
| 9 | Sign-in wait (ELITEA-4458): resume with `mcp_auth_action` other than `authorize` / `skip` through the API. | 400 "mcp_auth_action must be authorize or skip". |
| 10 | As OW, check the run log and notices of the decided runs. | Only toolkit names; no URL, token or credential value. |

---

## Expected Final State

Every decision by a non-owner was refused; the owner's decisions applied once.

---

## Pass/Fail Criteria

**Pass:**
- Only the owner can decide, through every route.

**Fail:**
- Any non-owner (including a project admin) approves or rejects a waiting run.
