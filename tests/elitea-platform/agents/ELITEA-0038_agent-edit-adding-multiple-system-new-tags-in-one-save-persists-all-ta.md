---
id: ELITEA-0038
title: "[Agent Edit] Adding Multiple System-New Tags in One Save Persists All Tags"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [bug-env:next, feat:tags, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5151]
---
# ELITEA-0038: [Agent Edit] Adding Multiple System-New Tags in One Save Persists All Tags

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that adding 2 or more tags that have never been used anywhere in the system (system-new) to an existing agent in a single save operation correctly persists all of them.

**Coverage:**
- Core bug scenario: multiple system-new tags added in one save
- All tags survive hard page reload
- No tags silently discarded on save

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- An existing agent with no tags is available
- The tags in the test data must not exist anywhere in the system before this test (verify via tag autocomplete — no suggestions should appear)
- Browser: Chrome latest

## Test Data

- Tags to add: BrandNewTag_Alpha (system-new), BrandNewTag_Beta (system-new), BrandNewTag_Gamma (system-new)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents and open an existing agent that has no tags assigned. | Agent edit view opens; tag field is empty. |
| 2 | Add tag BrandNewTag_Alpha to the tag field. | Chip appears in the tag field. |
| 3 | Add tag BrandNewTag_Beta. | Second chip appears; 2 chips visible. |
| 4 | Add tag BrandNewTag_Gamma. | Third chip appears; 3 chips visible in total. |
| 5 | Click Save. | Save completes with no error message. |
| 6 | Hard-reload the page (Ctrl+Shift+R) and reopen the same agent. | Agent detail view loads from fresh state. |
| 7 | Inspect the tag field. | All 3 tags — BrandNewTag_Alpha, BrandNewTag_Beta, BrandNewTag_Gamma — are displayed. |

## Expected Final State

All 3 tags — BrandNewTag_Alpha, BrandNewTag_Beta, BrandNewTag_Gamma — are displayed.

## Pass/Fail Criteria

**Pass:**
- All 3 system-new tags are present after save and hard reload

**Fail:**
- Fewer than 3 tags shown — any tag silently discarded after save
