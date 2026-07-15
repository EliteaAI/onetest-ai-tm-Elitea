---
id: ELITEA-2023
title: "Pipeline Dashboard — Search"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2023: Pipeline Dashboard — Search

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Pipelines dashboard search box filters the pipeline list to show only pipelines matching the search term, and clears back to the full list when the search is cleared.

---

## Preconditions

- User is logged in to the Elitea platform.
- The Pipelines dashboard contains at least one pipeline whose name contains "YAML" (e.g., "YAML Validation").

---

## Test Data

| Field | Value |
|-------|-------|
| Search term | YAML |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipelines dashboard (/app/pipelines/all) | Pipelines dashboard loads with full list |
| 2 | Locate the search textbox with placeholder "Let's find something amazing!" | Search textbox is visible |
| 3 | Type "YAML" in the search box | Search input is populated with "YAML" |
| 4 | Verify filtered results show only pipelines containing "YAML" in their name (e.g., "YAML Validation") | Only matching pipelines are shown in the list |
| 5 | Clear search text | Search field is empty |
| 6 | Verify full pipeline list is restored | All pipelines are visible again |

---

## Expected Final State

The search filter correctly narrows the pipeline list to matching results and restores the full list when cleared.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Search correctly filters the list to matching pipelines and restores all pipelines when cleared.

**Fail:**
- Any step produces an error or unexpected result.
- Search shows incorrect results or does not clear properly.
