---
id: ELITEA-3894
title: "Upload and change custom icon on edit skill form with immediate reflection"
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
- At least one existing Skill exists (with or without custom icon)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Icon File | Valid image file under 500 KB (different from current icon if any) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills page via sidebar | Skills page loads |
| 2 | Click on an existing Skill to edit | Skill edit form opens |
| 3 | Click on the icon picker to open SelectIconDialog | SelectIconDialog modal opens |
| 4 | Upload a new image file or select a different existing icon | New icon is selected |
| 5 | Confirm the new icon and close the dialog | Dialog closes |
| 6 | **Without saving or refreshing the page**, observe the form | New icon is immediately visible in the form |
| 7 | Click **Save** | Skill saves successfully |
| 8 | Verify the updated icon persists after save | Updated icon is displayed |
| 9 | Navigate away from the Skill page | Navigation succeeds |
| 10 | Return to the Skill | Skill edit page loads |
| 11 | Verify the icon is still the updated one | Updated icon persists |

## Expected Final State

The Skill displays the new custom icon immediately upon selection (before save) and persists after saving and navigation.

## Pass/Fail Criteria

**Pass:**
- New icon reflects immediately without page reload
- Icon persists after save
- Icon persists after navigation away and back

**Fail:**
- Icon does not update until page refresh
- Icon reverts to previous after save
- Icon not persisted after navigation
