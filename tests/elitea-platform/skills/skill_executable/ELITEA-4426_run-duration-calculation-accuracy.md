---
id: ELITEA-4426
title: "Verify run duration calculation is accurate"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, duration, data-accuracy]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- Skill run has completed
- User is on analytics page
- Run has duration data

## Test Data

| Field | Value |
|-------|-------|
| Duration Format | Seconds with decimal (e.g., "9.52s", "1.65s") |
| Calculation | Time from first event start to last event end |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On analytics page, locate run duration display | Duration visible in header or Health tab |
| 2 | Note the duration value | Value shown (e.g., "9.52s") |
| 3 | Navigate to Health tab | Health tab opens |
| 4 | Observe individual event latencies | Latencies listed per event |
| 5 | Calculate total duration from first to last event | Manual calculation from timestamps/latencies |
| 6 | Compare calculated duration with displayed duration | Values match |
| 7 | Verify calculation includes all LLM, tool, skill events | All events counted |
| 8 | (Backend) Verify value matches usage_event execution time | DB value matches UI |

## Expected Final State

Run duration:
- Displayed clearly (e.g., "9.52s", "1.65s")
- Duration = time from first event start to last event end
- Includes all LLM, tool, and skill events
- Matches actual execution time in usage_event

## Pass/Fail Criteria

**Pass:**
- Duration displayed clearly
- Calculation accurate: first event to last event
- Includes all event types
- Value matches usage_event data
- Format correct (seconds with decimal)

**Fail:**
- Duration missing or unclear
- Calculation incorrect
- Missing event types in calculation
- Value doesn't match usage_event
- Format incorrect
