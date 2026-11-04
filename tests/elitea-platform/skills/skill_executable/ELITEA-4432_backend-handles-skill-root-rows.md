---
id: ELITEA-4432
title: "Verify backend correctly handles skill-root rows in run-scoped queries"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, backend, skill-root]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- Skill run has been executed and attributed to skill root entity (S7 dependency)
- usage_event table has rows with root_type = 'skill'
- Backend analytics endpoints operational

## Test Data

| Field | Value |
|-------|-------|
| Expected root_type | 'skill' (not 'agent' or 'pipeline') |
| Backend Service | usage service |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Query usage_event table for skill run | `SELECT * FROM usage_event WHERE run_id = '<skill_run_uuid>'` |
| 2 | Verify root_type field | root_type = 'skill' |
| 3 | Verify root_id field populated | Contains skill identifier |
| 4 | Verify root_version field populated | Contains skill version |
| 5 | Call analytics_run_detail endpoint with skill run scope | POST /analytics/run_detail with skill run_id |
| 6 | Verify response status | HTTP 200 OK |
| 7 | Verify response structure | JSON contains expected fields |
| 8 | Check response includes skill-specific fields | skill_id, skill_version present |
| 9 | Verify ordered LLM calls returned | LLM events in chronological order |
| 10 | Verify ordered tool calls returned | Tool events in chronological order |
| 11 | Verify skill events returned (S7) | Skill lifecycle events included |
| 12 | Verify metadata includes: model(s), tokens, cost, duration, errors | All metadata present |
| 13 | Verify no SQL errors in backend logs | No database errors |
| 14 | Verify response time < 2 seconds | Performance acceptable |

## Expected Final State

Backend skill-root handling:
- usage_event rows have root_type = 'skill'
- Backend accepts skill root in run scope
- analytics_run_detail returns:
  - Ordered LLM calls
  - Ordered tool calls
  - Skill events (S7)
  - skill_id, skill_version fields
  - Model(s), tokens, cost, duration, errors
- No SQL errors
- Response time < 2 seconds

## Pass/Fail Criteria

**Pass:**
- root_type = 'skill' in usage_event
- Backend accepts skill root scope
- API returns HTTP 200
- Response structure correct
- All required fields present
- LLM/tool calls ordered
- Skill events included
- No errors, good performance

**Fail:**
- root_type not 'skill'
- Backend rejects skill root scope
- API error response
- Missing fields in response
- LLM/tool calls not ordered
- Skill events missing
- SQL errors, poor performance
