---
id: ELITEA-4421
title: "Verify Health tab shows Failed Calls section with error details"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, health, errors]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- Skill run has completed with at least one error
- User is on Health tab of analytics page
- Errors are logged in usage_event table

## Test Data

| Field | Value |
|-------|-------|
| Table Columns | TIME, EVENT TYPE, MODEL / TOOL, LATENCY |
| Example Failed Call | `2026-10-14 12:24:46 \| llm \| test1 \| 406ms` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On Health tab, scroll down to "Failed Calls" section | Section appears (only if run has errors) |
| 2 | Observe table headers | Headers: TIME, EVENT TYPE, MODEL / TOOL, LATENCY |
| 3 | Verify table lists all failed events | Each failed call has a row |
| 4 | Check TIME column | Exact timestamp of failure (YYYY-MM-DD HH:MM:SS format) |
| 5 | Check EVENT TYPE column | Type of event that failed (e.g., "llm", "tool") |
| 6 | Check MODEL / TOOL column | Identifier of resource that failed (e.g., "test1", model name) |
| 7 | Check LATENCY column | Duration before failure (e.g., "406ms") |
| 8 | Verify error text is displayed in red color | Error indicators shown in red for visibility |
| 9 | (If expandable) Click on a failed call to view details | Error details/message displayed |
| 10 | Cross-reference with usage_event error logs | Details accurate and match DB error logs |

## Expected Final State

Failed Calls section displays:
- Appears only if run has errors
- Lists all failed events with timestamp
- TIME: exact timestamp (YYYY-MM-DD HH:MM:SS)
- EVENT TYPE: type of failed event
- MODEL / TOOL: resource identifier
- LATENCY: duration before failure (ms)
- Error text/indicators in red color
- Details match usage_event error logs

## Pass/Fail Criteria

**Pass:**
- Failed Calls section appears for runs with errors
- All failed events listed
- TIME accurate and formatted correctly
- EVENT TYPE accurate
- MODEL / TOOL shows correct identifier
- LATENCY accurate
- Errors highlighted in red
- Details match usage_event logs

**Fail:**
- Section missing for runs with errors
- Missing failed events
- Incorrect timestamps
- Wrong event types or identifiers
- Latency incorrect
- Errors not highlighted
- Details don't match usage_event logs
