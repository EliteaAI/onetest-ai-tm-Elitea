---
id: ELITEA-3461
title: "Reindex and batch indexing: usage is not double-counted; embedding model name and pricing captured correctly"
priority: medium
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, indexing, reindex, batch]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6570"]
---

# ELITEA-3461: Reindex and batch indexing: usage is not double-counted; embedding model name and pricing captured correctly

**Module:** usage-cost-tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that reindexing unchanged content and batch-indexing multiple documents produce consistent, non-double-counted `usage_event`/`usage_counter` records, and that the embedding model name is captured correctly with correct pricing applied — distinguishable by `model_name` if the embedding model configuration changes mid-deployment.

---

## Preconditions

- Logged in to {{base_url}}.
- Artifact or SharePoint toolkit configured with a bucket containing ≥3 documents for batch indexing.
- A previously indexed document available to reindex without content changes.

---

## Test Data

| Field | Value |
|-------|-------|
| Batch | ≥3 documents in one bucket |
| Reindex target | 1 previously indexed, unchanged document |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a reindex of the unchanged document (full reindex, per confirmed "Successful reindex replaces active index" behavior). | Reindex completes; the active index is replaced. |
| 2 | Inspect `usage_event` for the reindex. | Record whether unchanged content is fully re-embedded (full cost again) or skipped — document the actual observed behavior rather than assuming delta-only. |
| 3 | Re-run the same reindex a second time without further changes. | Reindex completes again. |
| 4 | Compare `usage_counter` totals across both reindex runs. | Usage is consistent and **not double-counted** — the idempotency key still applies correctly. |
| 5 | Batch-index the ≥3 documents in one operation. | Each document's usage is recorded as separate row(s) in `usage_event`. |
| 6 | Sum the individual per-document usage and compare to the `usage_counter` total for the batch. | Total matches the sum of individual records. |
| 7 | Inspect the embedding model name on any row. | Correct `model_name` captured with correct pricing applied. |

---

## Expected Final State

Reindex and batch operations produce internally consistent, correctly attributed, non-duplicated usage records with correct model/pricing metadata.

---

## Pass/Fail Criteria

**Pass:**
- Reindex usage is consistent and not double-counted across repeated runs.
- Batch total equals the sum of individual document rows.
- `model_name` and pricing are correct on all rows.

**Fail:**
- Repeated reindexing double-counts usage for the idempotency key.
- Batch total doesn't match the sum of individual rows.
- `model_name`/pricing is missing or incorrect.
