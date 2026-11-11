---
id: ELITEA-4506
title: "Paid Tools section formatting and labels are clear and consistent across usage states"
priority: medium
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4506: Paid Tools section formatting and labels are clear and consistent across usage states

**Module:** Usage Cost Tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm the "Paid Tools" block on Settings → Usage uses clear, consistent labels and formatting across different features/scenarios, since this is new UI with no prior documentation to benchmark against.

**Coverage:**
- Zero-usage empty state
- Partial-usage label/format correctness
- Progress bar visual consistency with the main project budget bar
- Multiple paid-tool features rendering without collision

## Preconditions

- Project has the paid-tool module enabled

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/usage` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | View the Paid Tools section with zero usage recorded for the feature. | Sensible empty/zero state shown (e.g. "$0.00 of $Y", "0 calls"), not a blank or broken row. |
| 2 | View it with partial usage. | Label wording ("Web search: $X of $Y"), call count phrasing ("N calls"), and description text ("Tracked separately from model usage...") render correctly without truncation or overlap at common screen widths. |
| 3 | Compare the progress bar color/style to the main project budget bar. | Visually consistent conventions (e.g. color change near/at limit). |
| 4 | If multiple paid-tool features exist simultaneously (e.g. Web Search plus a future second paid tool). | Each renders as its own distinct line without visual collision. |

## Expected Final State

Paid Tools section displays clearly and consistently across zero-usage, partial-usage, and multi-feature states.

## Pass/Fail Criteria

**Pass:**
- All states render clear, correctly formatted, non-overlapping content

**Fail:**
- Any state shows a blank/broken row, truncated/overlapping text, or visual collision between features
