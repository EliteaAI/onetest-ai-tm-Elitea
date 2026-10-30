---
id: ELITEA-4229
title: "Schedule Card Last Run Is Shown Per Index"
priority: low
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:indexer, feat:toolkits, eng:frontend, schedule, last-run]
requirements: [EliteaAI/elitea_issues#7083]
---
# ELITEA-4229: Schedule Card Last Run Is Shown Per Index

**Module:** Toolkits & Indexes · **Priority:** Low · **Type:** Functional

**Objective:** Verify that in a toolkit with several indexes, each index's schedule card shows the `Last run` of that index only.

**Coverage:**
- `Last run` is computed from the selected index's own history
- Switching between indexes does not carry over the previous index's value

## Preconditions

- A toolkit with two or more indexes, each with a schedule configured
- The indexes' most recent runs finished at different times

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the toolkit → Indexes → select Index A. | SCHEDULE card shows `Last run` matching Index A's newest History row. |
| 2 | Select Index B. | SCHEDULE card shows `Last run` matching Index B's newest History row (different from Index A). |
| 3 | Switch back to Index A. | `Last run` again shows Index A's value. |

## Expected Final State

Each index shows its own `Last run`.

## Pass/Fail Criteria

**Pass:**
- Each index's card shows the value from its own history

**Fail:**
- An index shows another index's `Last run`, or the value does not refresh when switching indexes
