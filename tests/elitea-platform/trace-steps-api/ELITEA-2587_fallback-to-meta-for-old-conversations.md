---
id: ELITEA-2587
title: "Backfill migration verification: migrated vs non-migrated conversations"
priority: high
type: functional
module: trace-steps-api
status: ready
execution_type: manual
tags: [nfr:performance, eng:backend, epic:5724, regression]
requirements: [EliteaAI/elitea_issues#5724, EliteaAI/elitea_issues#5800]
---
# ELITEA-2587: Backfill migration verification: migrated vs non-migrated conversations

**Module:** Trace Steps API · **Priority:** High · **Type:** Functional

**Objective:** Verify that the backfill migration task (#5800) correctly migrated conversations within the 180-day window, and that conversations older than the cutoff remain unmigrated.

**Context:** Admin task `backfill_legacy_trace_steps` migrated conversations created within 180 days from migration date (15 July 2026). Cutoff date: **17 January 2026**. Conversations before this date were NOT migrated and remain in `meta`.

**Coverage:**
- Migrated conversations (after 16 Jan 2026): data in table, meta cleaned, marker present
- Non-migrated conversations (before 16 Jan 2026): no data in table, data remains in meta
- `/message_traces/` returns correct data or empty for respective groups

## Preconditions

- Logged in to {{base_url}}
- Access to conversations from different time periods
- Backfill migration task completed on DEV

## Test Data

| Field | Value |
|-------|-------|
| Migration date | 15 July 2026 |
| Cutoff window | 180 days |
| Cutoff date | **17 January 2026** |
| Migrated conversation | Created AFTER 17 January 2026 (e.g., March 2026, May 2026) |
| Non-migrated conversation | Created BEFORE 17 January 2026 (e.g., December 2025) |

## Steps

### Part A: Migrated Conversation (< 180 days old)

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Find conversation created AFTER 17 January 2026 with tool calls | Conversation exists (e.g., from March 2026 or May 2026) |
| 2 | Call `/message_traces/...` endpoint for this conversation | Returns `"rows": [...]` with tool_calls and/or thinking_steps |
| 3 | Call `/conversation/...` endpoint for same conversation | Response includes message_groups |
| 4 | Check `message_groups[].meta` for `tool_calls` key | Key is **NOT present** (migrated and stripped) |
| 5 | Check `message_groups[].meta` for `thinking_steps` key | Key is **NOT present** (migrated and stripped) |
| 6 | Check `message_groups[].meta` for `_migrated_trace_steps` marker | Marker **IS present** with timestamp and reason |
| 7 | Open conversation in UI | Tool calls and thinking steps are visible in UI (loaded from table) |

### Part B: Non-Migrated Conversation (> 180 days old)

| # | Action | Expected Result |
|---|--------|----------------|
| 8 | Find conversation created BEFORE 17 January 2026 with tool calls | Conversation exists (e.g., from December 2025) |
| 9 | Call `/message_traces/...` endpoint for this conversation | Returns `"rows": []` (empty, NOT migrated) |
| 10 | Call `/conversation/...` endpoint for same conversation | Response includes message_groups |
| 11 | Check `message_groups[].meta` for `tool_calls` key | Key **IS present** (NOT migrated, data remains in meta) |
| 12 | Check `message_groups[].meta` for `thinking_steps` key | Key **IS present** if conversation had thinking (NOT migrated) |
| 13 | Check `message_groups[].meta` for `_migrated_trace_steps` marker | Marker **NOT present** (conversation not migrated) |
| 14 | Open conversation in UI | **Known issue:** Tool calls may NOT be visible in UI (UI reads from `/message_traces/` only, not meta fallback) |

## Expected Final State

- **Migrated conversations:** Data in `message_trace_step` table, `meta` cleaned with migration marker
- **Non-migrated conversations (>180 days):** No data in table, data remains in `meta`, UI may not display tool calls (known limitation)

## Pass/Fail Criteria

**Pass:**
- Migrated: `/message_traces/` returns data, meta cleaned, marker present
- Non-migrated: `/message_traces/` returns empty, meta contains data, no marker
- Cutoff date (17 Jan 2026) correctly separates migrated/non-migrated

**Fail:**
- Migrated conversation has data in meta (not cleaned)
- Non-migrated conversation has data in table (should not be migrated)
- Marker missing on migrated conversations

## Notes

- **Known issue for Part B:** UI does not implement fallback to meta, so conversations older than 180 days lose UI visibility of tool calls/thinking steps even though data exists in meta.
- Migration window: 180 days from 15 July 2026 = cutoff at 17 January 2026
- **Example migrated conversation:** 16 March 2026 (project 406, conversation 3505) - verified with marker present and meta cleaned
