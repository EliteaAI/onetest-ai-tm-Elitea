---
id: ELITEA-0037
title: "[Agent Edit] Agent with 1 Saved Tag — Adding Multiple System-New Tags in One Save Persists All"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [bug-env:next, feat:tags, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5151]
---
# ELITEA-0037: [Agent Edit] Agent with 1 Saved Tag — Adding Multiple System-New Tags in One Save Persists All

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that an agent which already has one saved tag correctly accepts and persists multiple system-new tags added in a single save operation, with the existing tag also retained.

**Coverage:**
- Specific state: agent already has exactly 1 saved tag
- Adding 2 system-new tags to this agent in one save
- All 3 tags (1 existing + 2 new) survive hard reload

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- An existing agent with exactly 1 already-saved tag: SavedTag
- The new tags must not exist anywhere in the system before this test
- Browser: Chrome latest

## Test Data

- Already-saved tag on agent: SavedTag
- System-new tags to add: BrandNewTag_New1 (system-new), BrandNewTag_New2 (system-new)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents and open the agent that has exactly 1 saved tag (SavedTag). | Agent edit view opens; tag field shows SavedTag. |
| 2 | Add tag BrandNewTag_New1 to the tag field. | Second chip appears; 2 chips visible. |
| 3 | Add tag BrandNewTag_New2. | Third chip appears; 3 chips visible. |
| 4 | Click Save. | Save completes with no error. |
| 5 | Hard-reload the page and reopen the same agent. | Agent detail view loads from fresh state. |
| 6 | Inspect the tag field. | All 3 tags — SavedTag, BrandNewTag_New1, BrandNewTag_New2 — are present. |

## Expected Final State

All 3 tags — SavedTag, BrandNewTag_New1, BrandNewTag_New2 — are present.

## Pass/Fail Criteria

**Pass:**
- All 3 tags present after save and hard reload

**Fail:**
- BrandNewTag_New1 or BrandNewTag_New2 missing; only SavedTag remains
