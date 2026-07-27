---
id: ELITEA-2501
title: "Deleting an uploaded icon reverts skills using it to default icon"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Admin or Editor role
- A Skill with a custom icon exists
- The Skill is attached to an Agent

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Skill | Skill with custom icon assigned |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload a custom icon and assign it to a Skill | Skill has custom icon |
| 2 | Note the icon filename/identifier | Identifier recorded |
| 3 | Open SelectIconDialog on any Skill | Dialog opens |
| 4 | Navigate to the uploaded icons gallery | Gallery displayed |
| 5 | Locate and delete the previously uploaded icon | Icon deleted |
| 6 | Navigate to the Skill that was using the deleted icon | Skill page loads |
| 7 | Verify the Skill now displays the default `skill-icon.svg` | Default icon shown |
| 8 | Check Skills list page | Default icon shown on card |
| 9 | Check Agent SKILLS section (if attached) | Default icon shown in SkillCard |
| 10 | Check SkillMenu dropdown | Default icon shown in dropdown |
| 11 | Check `~mention` autocomplete in Chat | Default icon shown in autocomplete |

## Expected Final State

When a user deletes an uploaded icon from the gallery, any Skills using that icon automatically revert to displaying the default `skill-icon.svg` across all UI locations.

## Pass/Fail Criteria

**Pass:**
- Icon deleted from gallery successfully
- Skill reverts to default icon
- Default icon displays consistently in all UI locations

**Fail:**
- Broken image shown after deletion
- Skill retains reference to deleted icon
- Inconsistent fallback across UI locations
