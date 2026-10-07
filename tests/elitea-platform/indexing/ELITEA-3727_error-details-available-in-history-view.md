---
id: ELITEA-3727
title: "Verify error details are available in History view"
priority: medium
type: functional
module: indexes
status: ready
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Index has a failed run in its history

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to index with failed run history | Index page displays |
| 2 | Open History view | History shows past runs |
| 3 | Locate the failed run entry | Failed run is visible |
| 4 | Expand or click on failed run | Error details are accessible |
| 5 | Review error information | Detailed error information is shown |

## Expected Final State

Users can access detailed error information for failed runs through the History view.

## Pass/Fail Criteria

**Pass:**
- Error details are accessible in History view
- Details provide useful diagnostic information

**Fail:**
- No error details available for failed runs
- Only generic "failed" status shown with no detail
