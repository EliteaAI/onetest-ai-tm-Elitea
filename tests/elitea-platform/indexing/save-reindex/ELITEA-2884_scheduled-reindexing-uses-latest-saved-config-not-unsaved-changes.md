---
id: ELITEA-2884
title: "Scheduled reindexing uses latest saved config not unsaved changes"
priority: critical
type: functional
module: indexing/save-reindex
status: ready
execution_type: manual
tags: [feat:indexer, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2884: Scheduled reindexing uses latest saved config not unsaved changes

**Module:** indexing/save-reindex · **Priority:** critical · **Type:** functional

**Objective:** 

---


## Preconditions

- User is logged in to `{{base_url}}`
- An existing index with an active indexing schedule (e.g., runs every 5 minutes for testing)
- Index has previously indexed data with a known configuration

## Test Data

| Field | Value |
|-------|-------|
| Saved Progress Step | 50 |
| Unsaved Progress Step | 99 |
| Schedule | Every 5 minutes (for testing) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an existing index, verify saved Progress Step is 50 | Configuration shows Progress Step = 50 |
| 2 | Verify indexing schedule is active | Schedule section shows active schedule |
| 3 | Modify Progress Step to 99 but do NOT click Save | "Save" and "Save & Reindex" buttons appear |
| 4 | Wait for the scheduled indexing to trigger | Scheduled indexing starts automatically |
| 5 | After scheduled indexing completes, check the index run history/details | Indexing was performed using Progress Step = 50 (saved value), NOT 99 |
| 6 | Verify Configuration tab still shows unsaved changes | Progress Step slider shows 99 (unsaved), buttons still present |

## Expected Final State

Scheduled reindexing uses the last saved configuration (Progress Step = 50), ignoring unsaved UI changes (99).

## Pass/Fail Criteria

**Pass:**
- Scheduled reindex uses saved config (50), not unsaved (99)
- Unsaved changes remain in UI after scheduled run
- No data corruption

**Fail:**
- Scheduled reindex uses unsaved config
- Unsaved changes are lost after scheduled run
- Configuration state becomes inconsistent
