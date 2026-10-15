---
id: ELITEA-3757
title: "Costs by model shows an \"Other models\" row and still adds up to the total"
priority: medium
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, costs, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#7000"]
---

# ELITEA-3757: Costs by model shows an "Other models" row and still adds up to the total

**Module:** analytics · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when more models were used than the breakdown shows, the rest is grouped into an "Other models" row and the rows add up to the total cost.

---

## Preconditions

- A project and window where more models were used than the Costs breakdown displays (the display limit).

---

## Test Data

| Field | Value |
|-------|-------|
| Window | A period with many models used |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Analytics → Costs for the window (or call `analytics_costs`). | The breakdown shows the top models plus an "Other models" row. |
| 2 | Sum Total Cost over all rows, including "Other models". | Equal to the Total Cost KPI. |
| 3 | Sum tokens over all rows. | Equal to the Total Tokens KPI. |
| 4 | Check "Other agents" / "Other users" when those exceed their limits too. | Same grouping; rows add up. |

---

## Expected Final State

No cost or tokens are hidden from the breakdown.

---

## Pass/Fail Criteria

**Pass:**
- Rows including "Other" add up exactly to the KPIs.

**Fail:**
- Rows add up to less than the total, or the "Other" row is missing or shows 0.
