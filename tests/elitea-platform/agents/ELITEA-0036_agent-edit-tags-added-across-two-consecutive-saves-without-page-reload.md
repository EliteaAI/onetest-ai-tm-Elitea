---
id: ELITEA-0036
title: "[Agent Edit] Tags Added Across Two Consecutive Saves Without Page Reload Are All Persisted"
priority: medium
type: functional
module: agents
status: ready
execution_type: manual
tags: [bug-env:next, feat:tags, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5151]
---
# ELITEA-0036: [Agent Edit] Tags Added Across Two Consecutive Saves Without Page Reload Are All Persisted

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that adding tags in one save, then adding more tags in a subsequent save without reloading the page between saves, results in all tags being correctly persisted.

**Coverage:**
- Consecutive save operations without intermediate page reload
- Mix of system-existing and system-new tags across the two saves
- All tags from both saves survive hard reload

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- An existing agent with no tags is available
- Identify 1 tag already in use in the system (system-existing)
- The system-new tags must not exist anywhere in the system before this test
- Browser: Chrome latest

## Test Data

- First save tags: ExistingSystemTag1 (system-existing), BrandNewTag_Consec1 (system-new)
- Second save tag (no page reload between saves): BrandNewTag_Consec2 (system-new)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents and open an existing agent with no tags. | Agent edit view opens; tag field is empty. |
| 2 | Add ExistingSystemTag1 and BrandNewTag_Consec1 to the tag field. | 2 chips visible in the tag field. |
| 3 | Click Save. | Save completes; both chips remain visible in the field. |
| 4 | Without reloading the page, add BrandNewTag_Consec2 to the tag field. | Third chip appears; 3 chips visible. |
| 5 | Click Save. | Save completes with no error. |
| 6 | Hard-reload the page and reopen the same agent. | Agent detail view loads from fresh state. |
| 7 | Inspect the tag field. | All 3 tags — ExistingSystemTag1, BrandNewTag_Consec1, BrandNewTag_Consec2 — are present. |

## Expected Final State

All 3 tags — ExistingSystemTag1, BrandNewTag_Consec1, BrandNewTag_Consec2 — are present.

## Pass/Fail Criteria

**Pass:**
- All 3 tags present after consecutive saves and hard reload
- No page reload required between saves to maintain correct behavior

**Fail:**
- Any tag missing after reload
