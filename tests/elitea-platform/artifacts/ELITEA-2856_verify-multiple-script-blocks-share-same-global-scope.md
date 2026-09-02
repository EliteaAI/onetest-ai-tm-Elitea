---
id: ELITEA-2856
title: "Verify multiple <script> blocks share the same global scope"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, comm:feedback, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6176]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An artifact bucket exists and is available for file upload

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | `multi-script-scope.html` — a variable declared in one `<script>` block is read in a later block |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `multi-script-scope.html` and open in Preview mode | Page renders the test result |
| 2 | Observe the result | Second script block successfully reads the variable set by the first |
| 3 | Confirm the reported verdict | Shows **PASS — global scope shared** |

## Expected Final State

Multiple inline `<script>` blocks on the same page share one global scope, matching normal browser behavior.

## Pass/Fail Criteria

**Pass:**
- Result shows PASS — global scope shared

**Fail:**
- Second script block cannot read the variable set by the first (scope is isolated per block)
