---
id: ELITEA-2995
title: "Jira execute_generic_rq – Raw PUT /rest/api/3/issue/{key} With fields= ADF description Succeeds (204, Workaround Confirmed)"
priority: high
type: functional
module: jira
status: draft
execution_type: manual
tags: [sdk, jira, execute-generic-rq, adf, issue:5856]
requirements: [EliteaAI/elitea_issues#5856]
---

# ELITEA-2995: Jira execute_generic_rq – Raw PUT /rest/api/3/issue/{key} With fields= ADF description Succeeds (204, Workaround Confirmed)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Verify that bypassing the SDK's `update=` operations-format routing and instead issuing a raw `PUT /rest/api/3/issue/{key}` request via `execute_generic_rq` with a `fields`-style body (same ADF `description` payload that fails via `update_issue`) succeeds, confirming the failure in [[ELITEA-2994]] is specific to the SDK's `update=` routing rather than the ADF payload itself or the Jira API.

---

## Preconditions

- Jira toolkit is configured with valid credentials against a Cloud v3 (ADF-capable) deployment.
- A test issue exists (e.g. `CRM-5`) that can be safely updated.

---

## Test Data

| Field | Value |
|-------|-------|
| Issue key | `CRM-5` |
| Method | `execute_generic_rq` |
| Request | `PUT /rest/api/3/issue/CRM-5` |
| Body | `{"fields": {"description": <same ADF doc as ELITEA-2994: H2 heading + bold paragraph + bullet list>}}` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `execute_generic_rq` to issue a raw `PUT /rest/api/3/issue/CRM-5` with the `fields`-style body containing the ADF description | Call succeeds with `204 No Content` |
| 2 | Re-read the issue (`get_issue` or equivalent) | `description` reflects the submitted ADF content (heading, bold paragraph, bullet list all present) |

---

## Expected Final State

The raw v3 REST PUT with a `fields=`-style body applies the ADF description update successfully, confirming the ADF payload is valid and Jira-accepted.

---

## Pass/Fail Criteria

**Pass:** Request returns `204 No Content` and the re-read issue shows the updated ADF description.
**Fail:** Request fails, or the re-read issue does not reflect the submitted description — would indicate the workaround itself is unreliable and the root cause is not isolated to `update_issue`'s `update=` routing.
