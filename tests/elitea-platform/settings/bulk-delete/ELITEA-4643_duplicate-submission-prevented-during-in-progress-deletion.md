---
id: ELITEA-4643
title: "Duplicate submission of delete action is prevented during in-progress deletion"
priority: critical
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- Project with a large item count (dozens+) in at least one selected type
- API access/testing tool available for a parallel request

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity type with large count | Toolkits (or similar large-count type) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select one or more entity types, complete the typed-DELETE confirmation, and submit | Deletion begins; progress indicator shown |
| 2 | While deletion is in progress, attempt to click "Delete permanently" or "Delete selected data" again in the UI | Second submission prevented (button disabled/action blocked/ignored) |
| 3 | In parallel, send a second direct API call to the same delete endpoint for the same project while the first request is still processing | Second request rejected or safely queued; no duplicate deletion or corruption |
| 4 | Wait for the first deletion to complete | Completion reported normally with accurate counts |

## Expected Final State

Exactly one deletion operation is ever actually applied, regardless of duplicate UI clicks or a concurrent API call.

## Pass/Fail Criteria

**Pass:**
- No double-delete or data corruption occurs

**Fail:**
- A second submission is accepted and causes duplicate processing, an error, or inconsistent counts
