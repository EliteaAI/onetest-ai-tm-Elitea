---
id: ELITEA-3092
title: "Automated: Failed reindex preserves active index"
priority: critical
type: automated
module: indexing/reindex-preservation
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, automated, regression, reindex-preservation]
requirements: [EliteaAI/elitea_issues#6232]
---

# ELITEA-3092: Failed reindex preserves active index

**Module:** indexing/reindex-preservation · **Priority:** critical · **Type:** automated

**Objective:** Verify that when reindexing fails, the previously active index remains fully available and searchable with no data loss.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit index with ✅ Completed status and known content.
- Ability to trigger reindex failure (e.g., via API mock or credential revocation).

---

## Test Data

| Variable | Description |
|----------|-------------|
| `index_name` | Name of the test index |
| `document_count` | Number of documents in the index before test |
| `search_keyword` | Unique keyword for search verification |
| `failure_method` | Method to cause reindex failure |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Indexes tab. Select test index. Note `document_count`. | Index shows ✅ Completed with document count. |
| 2 | Perform search using `search_keyword`. Note results. | Search returns expected results. |
| 3 | Trigger reindex failure condition (e.g., invalidate credentials). | Failure condition set. |
| 4 | Initiate Reindex. Wait for failure. | Reindex fails with error message. |
| 5 | Verify error message contains "Previously indexed data remains available". | Message confirms data preservation. |
| 6 | Verify index status is ✅ Completed (not broken/error). | Status unchanged from before failure. |
| 7 | Verify document count is unchanged. | Count = `document_count`. |
| 8 | Perform same search as step 2. | Search returns identical results. |
| 9 | Restore credentials for cleanup. | Credentials restored. |

---

## Pass/Fail Criteria

**Pass:**
- Index status remains ✅ Completed after failure
- Document count unchanged
- Search returns identical results after failure
- Error message confirms data preservation

**Fail:**
- Index shows error/broken status
- Document count decreased or index empty
- Search fails or returns different results
- No data preservation confirmation
