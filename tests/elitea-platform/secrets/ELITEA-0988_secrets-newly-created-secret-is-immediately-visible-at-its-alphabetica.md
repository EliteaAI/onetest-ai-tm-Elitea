---
id: ELITEA-0988
title: "[Secrets] Newly Created Secret Is Immediately Visible at Its Alphabetical Position"
priority: critical
type: functional
module: secrets
status: ready
execution_type: manual
tags: [feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4866]
---
# ELITEA-0988: [Secrets] Newly Created Secret Is Immediately Visible at Its Alphabetical Position

**Module:** Secrets · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after creation completes, the newly created secret is findable at its correct alphabetical position without needing to reload or re-sort.

**Coverage:**
- New secret integrates into the A→Z sorted list after creation
- No manual reload or re-sort required to find the item
- Correct positioning in a multi-page list

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Enough secrets to span multiple pages (20+ secrets)
- Default sort is A→Z
- Browser: Chrome latest

## Test Data

- New secret name: ZebraTest (should appear near the end of alphabetical order)
- New secret value: ztest-value

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → Secrets. | Secrets list loads sorted A→Z. |
| 2 | Click Create, fill in name ZebraTest and value ztest-value, then save. | Secret is created successfully. |
| 3 | Navigate to the page where Z-named items appear (last page of the list). | Last page loads. |
| 4 | Locate ZebraTest in the list. | ZebraTest is present at its correct alphabetical position near the end of the list. |

## Expected Final State

ZebraTest is present at its correct alphabetical position near the end of the list.

## Pass/Fail Criteria

**Pass:**
- ZebraTest is findable at its expected alphabetical position without manual reload or re-sort

**Fail:**
- ZebraTest is not at its expected position
- User must reload the page or re-sort to find the newly created item
