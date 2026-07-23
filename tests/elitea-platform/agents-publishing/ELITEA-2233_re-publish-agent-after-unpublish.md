---
id: ELITEA-2233
title: "Re-publish agent after unpublish"
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
- Test agent previously published then unpublished
- Agent has 3 attached Skills: Alpha, Beta, Gamma

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "Unpublish Test Agent" |
| Current Status | Unpublished/Draft |
| Skills | Alpha, Beta, Gamma (3 total) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the unpublished agent | Agent loads with Skills |
| 2 | Verify 3 Skills attached | Alpha, Beta, Gamma visible |
| 3 | Click ⋮ menu → **Publish** | Publish wizard opens |
| 4 | Enter version: "1.1.0" | New version name |
| 5 | Complete Preparation step | Continue to Validation |
| 6 | Wait for validation | Result: **PASS** |
| 7 | Verify all 3 Skills validated | No Skills-related critical issues |
| 8 | Click **Publish** | "The agent has been published" toast |
| 9 | Navigate to Agent Hub | Hub loads |
| 10 | Search for agent | Agent appears in Hub again |
| 11 | Add to conversation and test | Agent works |
| 12 | Test each Skill's functionality | All 3 Skills functional |

## Expected Final State

Previously unpublished agent can be successfully re-published with all Skills intact. All Skills are validated during re-publish and function correctly in the new published version.

## Pass/Fail Criteria

**Pass:**
- Re-publishing includes all currently attached Skills
- Skills validated during re-publish
- Agent appears in Hub after re-publish
- All Skills functional in re-published version

**Fail:**
- Skills missing from re-published version
- Validation fails for previously valid Skills
- Skills not functional after re-publish
