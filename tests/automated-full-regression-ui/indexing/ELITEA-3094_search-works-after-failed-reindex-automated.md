---
id: ELITEA-3094
title: "Automated: Search works after failed reindex"
priority: critical
type: automated
module: indexing/reindex-preservation
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, regression, reindex-preservation]
requirements: [EliteaAI/elitea_issues#6232]
---

# ELITEA-3094: Search works after failed reindex

**Module:** indexing/reindex-preservation · **Priority:** critical · **Type:** automated

**Objective:** Verify that search functionality works exactly as before after a reindex failure — no degradation, no missing data, no errors.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit index with ✅ Completed status and substantial content.
- Ability to trigger reindex failure.

---

## Test Data

| Variable | Description |
|----------|-------------|
| `index_name` | Name of the test index |
| `search_queries` | Array of search queries with known results |
| `expected_results` | Expected result counts for each query |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Perform multiple search queries. Note exact results for each. | Results captured (counts, titles). |
| 2 | Measure search response time baseline. | Response time < 3 seconds. |
| 3 | Trigger reindex failure condition. | Failure condition set. |
| 4 | Initiate Reindex. Wait for failure. | Reindex fails. |
| 5 | Perform same search queries immediately after failure. | All queries return identical results to step 1. |
| 6 | Verify no "index unavailable" errors. | No errors, clean results. |
| 7 | Measure search response time after failure. | Response time similar to baseline. |
| 8 | Perform additional varied search queries. | All return expected results. |

---

## Pass/Fail Criteria

**Pass:**
- All search queries return identical results after failure
- No "index unavailable" or similar errors
- Response time not significantly degraded
- All search features work normally

**Fail:**
- Any query returns fewer/different results
- Error messages about index state
- Significant performance degradation (>3x baseline)
- Search functionality broken
