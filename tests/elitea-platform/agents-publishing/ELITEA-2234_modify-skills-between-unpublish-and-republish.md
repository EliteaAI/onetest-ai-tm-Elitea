---
id: ELITEA-2234
title: "Modify skills between unpublish and re-publish"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:skills, feat:agent-publishing, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5803]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has editor/admin role with publish permissions
- Test agent unpublished with 3 Skills: Alpha, Beta, Gamma
- Additional Skill "Delta" available to add

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "Skill Modify Test Agent" |
| Initial Skills | Alpha, Beta, Gamma |
| Skill to Add | Delta |
| Skill to Remove | Gamma |
| Skill to Modify | Alpha (content change) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open unpublished agent with Skills | Agent loads |
| 2 | Add new Skill "Delta Skill" | 4 Skills now attached |
| 3 | Remove "Gamma Skill" | 3 Skills: Alpha, Beta, Delta |
| 4 | Modify "Alpha Skill" content | Content updated |
| 5 | Click ⋮ menu → **Publish** | Wizard opens |
| 6 | Enter version: "2.0.0" | New version |
| 7 | Complete Preparation step | Validation runs |
| 8 | Verify validation includes modified Skills | All 3 current Skills validated |
| 9 | Complete validation and publish | Publishes successfully |
| 10 | Navigate to Agent Hub | Hub loads |
| 11 | Add published agent to conversation | Agent ready |
| 12 | Test "Alpha Skill" functionality | Uses MODIFIED content |
| 13 | Test "Beta Skill" functionality | Works (unchanged) |
| 14 | Test "Delta Skill" functionality | Works (newly added) |
| 15 | Verify "Gamma Skill" not present | Removed Skill NOT in published version |

## Expected Final State

Skill modifications (add, remove, edit) made between unpublish and re-publish are correctly reflected in the new published version. Added, removed, and modified Skills behave as expected.

## Pass/Fail Criteria

**Pass:**
- Added Skill (Delta) included in new published version
- Removed Skill (Gamma) NOT in new published version
- Modified Skill (Alpha) uses updated content
- Unchanged Skill (Beta) works as before
- Version history tracks Skill changes across publish cycles

**Fail:**
- Skill modifications not reflected in published version
- Removed Skill still present
- Modified content not used
