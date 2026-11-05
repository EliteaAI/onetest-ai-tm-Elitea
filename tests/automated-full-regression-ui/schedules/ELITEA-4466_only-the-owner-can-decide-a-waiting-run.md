---
id: ELITEA-4466
title: "Schedules — Only the Owner Can Decide a Waiting Run; a Run With a Chat Is Decided in Its Chat"
priority: critical
type: regression
module: schedules
status: draft
execution_type: manual
tags: [automated:API:regression, feat:schedules, nfr:security, issue:7304, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7304"]
---

# ELITEA-4466: Schedules — Only the Owner Can Decide a Waiting Run; a Run With a Chat Is Decided in Its Chat

**Module:** schedules · **Priority:** critical · **Type:** regression

**Objective:** Regression of the decision route permissions (#7304). Manual source: ELITEA-4461.

---

## Preconditions

- JWTs of the schedule **owner**, a **project admin**, an **editor** and a **viewer** of the same team project.
- A credential-wait run (as in ELITEA-4465 step 1) and a sensitive-tool waiting run with a chat (as in ELITEA-4467 step 3) of the owner's schedules.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As the project admin, decide the credential-wait run (`approve`). | 403 "Only the schedule owner can approve or reject this run"; still waiting. |
| 2 | As the editor and as the viewer, the same. | 403 each time. |
| 3 | As the owner, decide the sensitive-tool run through the decision route. | 409 "Decide this run in its chat". |
| 4 | As the owner, reject the credential-wait run. | 200; `failed` "rejected by the owner". |

---

## Expected Final State

Only the owner's decision applied.

## Teardown

Reject any waiting run; delete the schedules.
