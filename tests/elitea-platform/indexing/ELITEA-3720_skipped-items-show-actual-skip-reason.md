---
id: ELITEA-3720
title: "Verify skipped items show actual skip reason"
priority: high
type: functional
module: indexes
status: ready
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Data source contains items that will be skipped for various reasons

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Skip reasons | Unsupported format, Permission denied, File too large, Empty content |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start indexing with a source containing skippable items | Indexing completes with some skipped items |
| 2 | View index results | Skipped count is displayed |
| 3 | Check skipped items breakdown | Reason for skipping is shown (not generic "unsupported format") |
| 4 | Verify reasons are specific | Each skip reason matches the actual cause |

## Expected Final State

Skipped items display specific reasons (e.g., "Permission denied", "File too large") instead of generic text.

## Pass/Fail Criteria

**Pass:**
- Skipped items show specific, accurate reasons
- Different skip reasons are distinguished

**Fail:**
- All skipped items show "unsupported format" regardless of actual reason
- No reason is provided for skipped items
