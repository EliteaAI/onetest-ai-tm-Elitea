---
id: ELITEA-2944
title: "New Index — Cancel Discards Without Creating an Index"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, new-index, negative]
requirements: []
---
# ELITEA-2944: New Index — Cancel Discards Without Creating an Index

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking "Cancel" on the New Index page returns to the Toolkit details page and creates no Index.

**Coverage:**
- "Cancel" returns to the Toolkit details page
- No Index is created

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with zero existing Indexes

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any indexable toolkit with no existing Indexes |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Toolkit details page and inspect the Indexes panel. | Indexes panel shows no Indexes. |
| 2 | Click "+ Index". | The New Index page opens. |
| 3 | Enter any data needed to reach the point where "Index" becomes available. | Fields accept the entered values. |
| 4 | Click "Cancel". | User returns to the Toolkit details page. |
| 5 | Inspect the Indexes panel. | Indexes panel still shows no Indexes. |

## Expected Final State

The toolkit has the same number of Indexes as before the New Index page was opened.

## Pass/Fail Criteria

**Pass:**
- "Cancel" returns to the Toolkit details page
- No Index is created

**Fail:**
- An Index is created despite clicking "Cancel"
- "Cancel" navigates anywhere other than the Toolkit details page
