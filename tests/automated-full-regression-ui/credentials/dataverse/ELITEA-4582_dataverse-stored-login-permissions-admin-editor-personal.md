---
id: ELITEA-4582
title: "Dataverse — stored login permissions by API: editor 403, admin and personal owner allowed"
priority: critical
type: regression
module: toolkits-credentials/dataverse
status: draft
execution_type: manual
tags: [automated:API:regression, feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8, nfr:security]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4582: Dataverse — stored login permissions by API: editor 403, admin and personal owner allowed

**Module:** toolkits-credentials/dataverse · **Priority:** Critical · **Type:** Regression

**Objective:** API regression: only project admins can add or remove the saved login on a team Dataverse credential; the owner can on a personal credential. Manual source: ELITEA-4570.

---

## Preconditions

- JWTs of a project admin **ADM** and an editor **ED** of team project **P**.
- A Dataverse credential **C** in P.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As ED, POST a new Dataverse credential with `refresh_token`. | 403 "Only project admins can log in or out on a team credential". |
| 2 | As ED, PUT C adding `refresh_token`. | 403 (same message). |
| 3 | As ED, PUT C changing only the label. | 200. |
| 4 | As ADM, PUT C with `refresh_token`, then without it. | 200 both times. |
| 5 | As ED, PUT C removing a saved `refresh_token`. | 403. |
| 6 | As ED, in ED's personal project, POST a Dataverse credential with `refresh_token`, then remove it. | 200 both times. |

---

## Expected Final State

Test credentials deleted.

---

## Pass/Fail Criteria

**Pass:**
- Permissions as above.

**Fail:**
- An editor can change the saved login of a team credential.
