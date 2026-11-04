---
id: ELITEA-4433
title: "Verify analytics_run_detail API endpoint returns correct skill run data"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, backend, api]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- usage service is running and accessible
- Skill run data exists in database
- API endpoint: POST /analytics/run_detail

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | POST /analytics/run_detail |
| Request Body | `{ "run_scope": { "type": "run", "run_id": "<skill_run_uuid>" } }` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Prepare API request with skill run_id | Request body structured correctly |
| 2 | Make API call: POST /analytics/run_detail | Request sent |
| 3 | Observe HTTP response status code | HTTP 200 OK |
| 4 | Parse response JSON | Valid JSON returned |
| 5 | Verify `llm_calls` array present | Array of LLM events exists |
| 6 | Verify LLM calls chronologically ordered | Events in time order |
| 7 | Verify `tool_calls` array present | Array of tool events exists |
| 8 | Verify tool calls chronologically ordered | Events in time order |
| 9 | Verify `skill_events` array present | Array of skill lifecycle events exists (S7) |
| 10 | Verify `metadata` object present | Metadata object exists |
| 11 | Check metadata contains: skill_id | skill_id field populated |
| 12 | Check metadata contains: skill_version | skill_version field populated |
| 13 | Check metadata contains: model | Model name present |
| 14 | Check metadata contains: tokens (input, output, cache) | Token counts present |
| 15 | Check metadata contains: cost | Cost breakdown present |
| 16 | Check metadata contains: duration | Duration value present |
| 17 | Check metadata contains: errors | Error information present (if applicable) |
| 18 | Verify all timestamps in correct format | ISO 8601 or similar standard format |
| 19 | Verify data completeness | All expected fields populated |
| 20 | Verify data accuracy against usage_event table | Values match database |

## Expected Final State

API response contains:
- HTTP 200 OK
- Valid JSON structure
- `llm_calls`: chronologically ordered LLM events
- `tool_calls`: chronologically ordered tool events
- `skill_events`: skill lifecycle events (S7)
- `metadata`: { skill_id, skill_version, model, tokens, cost, duration, errors }
- All timestamps in correct format
- Data complete and accurate

## Pass/Fail Criteria

**Pass:**
- HTTP 200 response
- Valid JSON structure
- All arrays present: llm_calls, tool_calls, skill_events
- Events chronologically ordered
- Metadata complete with all fields
- Timestamps formatted correctly
- Data accurate vs database

**Fail:**
- Non-200 response
- Invalid JSON or errors
- Missing arrays
- Events not ordered
- Incomplete metadata
- Incorrect timestamp format
- Data inaccurate
