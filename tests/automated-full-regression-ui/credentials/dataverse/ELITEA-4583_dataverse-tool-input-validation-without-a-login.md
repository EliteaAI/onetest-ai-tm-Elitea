---
id: ELITEA-4583
title: "Dataverse — tool input checks that run before any Dataverse call"
priority: medium
type: regression
module: toolkits-credentials/dataverse
status: draft
execution_type: manual
tags: [automated:API:regression, feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4583: Dataverse — tool input checks that run before any Dataverse call

**Module:** toolkits-credentials/dataverse · **Priority:** Medium · **Type:** Regression

**Objective:** Regression of the Dataverse tool input checks. They run before the token is fetched, so no Microsoft login or Dataverse data is needed. Manual source: ELITEA-4572, 4573, 4576.

---

## Preconditions

- A Dataverse toolkit with any credential (no login needed).
- Run each tool from the toolkit Test settings or the tool run API.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | get_record record_id `123`. | "record_id must be a GUID". |
| 2 | get_record entity_set `a?b`. | "entity_set must be a Dataverse entity set name…". |
| 3 | get_record select `a;b`. | "select must be a comma-separated list of column logical names". |
| 4 | update_record fields `{}`. | "fields must be a non-empty object…". |
| 5 | update_record 21 fields. | "At most 20 columns per update". |
| 6 | update_record `ownerid`, `statecode`. | "'<column>' cannot be updated with this tool". |
| 7 | update_record a list value. | "…use a plain value (multi-select choices as '1,2')". |
| 8 | update_record `_x_value`; bind key with value `accounts(<guid>)`. | The two lookup messages. |
| 9 | query_records top 0 and 51. | Refused by the schema (1 to 50) or clamped (as recorded in ELITEA-4573). |
| 10 | who_am_i with no login. | Asks for a login ("Not logged in to Dataverse: use the Login button on the credential." or the sign-in prompt, see #7497). |

---

## Expected Final State

No change.

---

## Pass/Fail Criteria

**Pass:**
- Every check returns its message.

**Fail:**
- An invalid input reaches Dataverse.
