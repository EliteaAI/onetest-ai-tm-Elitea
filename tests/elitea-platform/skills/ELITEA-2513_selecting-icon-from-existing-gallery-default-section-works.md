---
id: ELITEA-2513
title: "Selecting icon from existing gallery default section works for skills"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Admin or Editor role
- Default/system icons exist in the gallery

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open SelectIconDialog from a Skill form | Dialog opens |
| 2 | Navigate to the "Default" section showing system/pre-existing icons | Default icons visible |
| 3 | Select one of the default icons | Icon selected |
| 4 | Confirm the selection and close the dialog | Dialog closes, icon applied |
| 5 | Verify the selected default icon is applied to the Skill in the form | Icon displayed |
| 6 | Save the Skill | Save succeeds |
| 7 | Verify the icon persists after save | Icon retained |

## Expected Final State

Users can select a pre-existing system icon from the "Default" section for a Skill.

## Pass/Fail Criteria

**Pass:**
- Default icons visible in gallery
- Selection applies to Skill
- Icon persists after save

**Fail:**
- Default section missing
- Selection not applied
- Icon not saved
