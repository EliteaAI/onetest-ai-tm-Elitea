---
id: ELITEA-2993
title: "ADO Work Item Text Search – Systematic Near-Miss Casing Sweep Across All Four Filters"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, new]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2993: ADO Work Item Text Search – Systematic Near-Miss Casing Sweep Across All Four Filters

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Extend the confirmed case-insensitivity finding ([[ELITEA-2967]], previously checked only for `work_item_type` and `state`) to `assigned_to` and `area_path` as well, for a complete picture of where case-insensitive matching applies across all four filters.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- Known values exist for a work item's assignee display name and area path, in their canonical ADO casing.

---

## Test Data

| Filter | Canonical-case value | Deliberately-mismatched-case value |
|--------|------------------------|--------------------------------------|
| assigned_to | `["<Known Name>"]` | `["<known name>"]` (all lowercase) |
| area_path | `["<Known\\Area\\Path>"]` | `["<known\\area\\path>"]` (all lowercase) |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `assigned_to` in canonical case, record `total_count` | Baseline count A |
| 2 | Call with `assigned_to` in mismatched case, record `total_count` | Count equals count A |
| 3 | Call with `area_path` in canonical case, record `total_count` | Baseline count B |
| 4 | Call with `area_path` in mismatched case, record `total_count` | Count equals count B |

---

## Expected Final State

Case-insensitive matching is confirmed consistently across all four filters (`work_item_type`, `state`, `assigned_to`, `area_path`), not just the two originally tested.

---

## Pass/Fail Criteria

**Pass:** Result counts for `assigned_to` and `area_path` are identical regardless of casing, matching the behavior already confirmed for `work_item_type`/`state`.
**Fail:** Either `assigned_to` or `area_path` behaves case-sensitively, meaning the case-insensitivity finding does not apply uniformly across filters.
