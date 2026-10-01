---
id: ELITEA-3462
title: "Indexing usage attributes to the real end-user or a resolvable system user (never NULL); background jobs still record after navigating away"
priority: medium
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, indexing, attribution]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6568"]
---

# ELITEA-3462: Indexing usage attributes to the real end-user or a resolvable system user (never NULL); background jobs still record after navigating away

**Module:** usage-cost-tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that indexing triggered by an end-user upload attributes usage to that end-user, and indexing triggered by an admin/system job attributes to a resolvable system/service user (never NULL, per #6568's "walk the user ladder": trigger creator → entity owner → system user). Also verify that usage for a background indexing job started before navigating away is still recorded once the job completes.

---

## Preconditions

- Logged in to {{base_url}} as a known test user.
- Ability to trigger indexing both directly as an end-user (file upload) and via an admin/system-level job if available in the test environment.

---

## Test Data

| Field | Value |
|-------|-------|
| End-user action | Upload + index a document as the known test user |
| System-triggered action | Any admin/system-initiated indexing job available in the environment |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As the known test user, upload a document and trigger indexing. | Indexing completes. |
| 2 | Inspect the resulting `usage_event` row's attribution. | Usage is attributed to the real end-user who triggered it. |
| 3 | Trigger an admin/system-initiated indexing job (if available). | Job runs. |
| 4 | Inspect the resulting row's attribution. | Usage attributes to a resolvable system/service user — never NULL. |
| 5 | Start a large/slow indexing job as the end-user, then immediately navigate away from the page before it completes. | Job continues running in the background (confirmed existing "Background Indexing Continues Across Navigation" behavior). |
| 6 | After the job completes, check `usage_event` for the corresponding row. | Usage for the job is recorded correctly despite the navigation away. |

---

## Expected Final State

Indexing usage is always attributed to a real, resolvable user (end-user or system), and background jobs record usage correctly regardless of navigation.

---

## Pass/Fail Criteria

**Pass:**
- End-user-triggered indexing attributes to that user; system-triggered indexing attributes to a resolvable system user.
- Background job started before navigating away still records usage once it completes.

**Fail:**
- Any indexing usage row has a NULL or unresolvable attribution.
- Usage for a background job is lost after navigating away.
