---
id: ELITEA-4439
title: "Verify graceful error handling for missing or invalid run_id"
priority: high
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, error-handling, edge-case]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User can manually craft or access invalid analytics URLs
- Error handling implemented in frontend and backend

## Test Data

| Field | Value |
|-------|-------|
| Invalid URL Example | `/skills/costs/skill123/history/analytics?run_id=invalid-uuid` |
| Expected Error Message | "Run not found" or "Unable to load analytics data" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Manually craft URL with invalid/non-existent run_id | URL prepared |
| 2 | Example: `/skills/costs/skill123/history/analytics?run_id=99999` | Invalid run_id in URL |
| 3 | Navigate to that URL in browser | Navigation attempted |
| 4 | Observe error handling | Error message or state displayed |
| 5 | Verify graceful error message appears | Message: "Run not found" or similar |
| 6 | Verify no application crash | App remains stable |
| 7 | Verify no blank white screen | Proper error UI shown |
| 8 | Verify breadcrumbs still work | Navigation available |
| 9 | Click breadcrumb to navigate back | Back navigation works |
| 10 | OR use browser Back button | Back button works |
| 11 | Verify no sensitive error details exposed | No DB stack trace, no internal IDs |
| 12 | Check console for errors (informational only) | Controlled error logging |

## Expected Final State

Error handling:
- Graceful error message: "Run not found" or "Unable to load analytics data"
- No application crash
- No blank white screen
- User can navigate back using breadcrumbs or browser Back
- No sensitive error details exposed

## Pass/Fail Criteria

**Pass:**
- Graceful error message displayed
- No crash or blank screen
- Navigation available (breadcrumbs/Back)
- No sensitive info exposed
- UI remains stable

**Fail:**
- No error message or unclear message
- Application crashes
- Blank white screen
- Navigation broken
- Sensitive error details exposed (DB trace, internal IDs)
- UI breaks or becomes unusable
