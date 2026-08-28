---
id: ELITEA-2900
title: "New Index Page — Breadcrumb and Field-Validation Gating on Index Action"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, new-index, validation]
requirements: []
---
# ELITEA-2900: New Index Page — Breadcrumb and Field-Validation Gating on Index Action

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify the dedicated New Index page shows the correct breadcrumb path, and that the "Index" action stays unavailable until all required fields are completed.

**Coverage:**
- Breadcrumb shows "Toolkits & Indexes / [Toolkit name] / New Index"
- "Index" action is unavailable with no data entered
- "Index" action remains unavailable while any required field is incomplete
- "Index" action becomes available once all required fields are valid

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit that supports indexing and has valid source data available

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any indexable toolkit with valid source data |
| Index Name | "validation-test-index" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Toolkit details page and click "+ Index". | Dedicated New Index page opens. |
| 2 | Inspect the breadcrumb. | Breadcrumb shows "Toolkits & Indexes / [Toolkit name] / New Index". |
| 3 | Without entering any data, inspect the "Index" action. | "Index" is disabled/unavailable. |
| 4 | Enter an Index name only, leaving other required fields incomplete. | "Index" remains disabled/unavailable. |
| 5 | Complete the remaining required fields under Index Configuration. | All required fields show valid values. |
| 6 | Inspect the "Index" action. | "Index" becomes enabled/available. |
| 7 | Click "Index". | Index is created; Index details page opens. |

## Expected Final State

The New Index page shows the correct breadcrumb, and the Index action is disabled until the form is fully valid.

## Pass/Fail Criteria

**Pass:**
- Breadcrumb matches the expected path
- "Index" stays disabled until all required fields are valid
- "Index" becomes enabled once the form is complete

**Fail:**
- Breadcrumb missing or incorrect
- "Index" is enabled before required fields are complete
- "Index" never becomes enabled once fields are valid
