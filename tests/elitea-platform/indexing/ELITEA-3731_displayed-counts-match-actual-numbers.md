---
id: ELITEA-3731
title: "Verify displayed counts match actual indexed/skipped/failed numbers"
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
- User has completed an indexing run with known results

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Known source count | Pre-counted documents in source |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note the total items in data source | Count recorded |
| 2 | Run indexing | Indexing completes |
| 3 | View indexed count in UI | Count displayed |
| 4 | View skipped count in UI | Skipped count displayed |
| 5 | Verify: indexed + skipped + failed = total source items | Counts add up correctly |

## Expected Final State

All displayed counts (indexed, skipped, failed) are accurate and consistent with source data.

## Pass/Fail Criteria

**Pass:**
- Indexed + skipped + failed = total source items
- Each individual count is accurate

**Fail:**
- Counts don't add up
- Numbers are missing or show as zero incorrectly
