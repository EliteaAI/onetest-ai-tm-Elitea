---
id: ELITEA-4405
title: "Same skill cannot be added twice to one template"
priority: critical
type: functional
module: chat-templates/skills
status: ready
execution_type: manual
tags: [user_story:6925, feat:skills, feat:chat-templates, skills-in-templates, duplicate-prevention]
requirements: [EliteaAI/elitea_issues#6925]
---
# ELITEA-4405: Prevent Duplicate Skill in Single Template

**Module:** Chat Templates / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the UI prevents adding the same skill twice to a single template through validation or disabled state.

## Preconditions

- At least one skill "Code Reviewer" exists in the project
- User is logged in as project admin

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Template Name | Duplicate Prevention Test |
| Skill | Code Reviewer |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General → Chat templates | Chat templates page loads |
| 2 | Click "+ Template" button and enter template name "Duplicate Prevention Test" | Create Template modal opens with name populated |
| 3 | Click in "Search participants..." field and select Skills tab | Skills tab activates |
| 4 | Search for "Code Reviewer" and add it | Skill chip appears in PARTICIPANTS section |
| 5 | Verify "Code Reviewer" appears as a chip in PARTICIPANTS section | Skill chip visible with icon and name |
| 6 | Click in "Search participants..." field again and go to Skills tab | Skills tab activates again |
| 7 | Search for "Code Reviewer" again | Skill appears in search results |
| 8 | Verify the skill is disabled, grayed out, or shows as already added | Skill visually indicates it's already added (disabled/grayed) |
| 9 | Click "Save" to save the template | Template saves successfully |
| 10 | Re-open the template and verify only ONE instance of "Code Reviewer" exists | Only one skill chip present |

## Expected Final State

- First addition of "Code Reviewer" succeeds
- Same skill appears only once in participant chips
- UI prevents duplicate addition (skill disabled/hidden in picker after first add)
- Or: Attempting to add duplicate shows validation message
- Template saves with only one instance of the skill
- No duplicate skill IDs in saved template data

## Pass/Fail Criteria

**Pass:**
- First skill addition succeeds
- Skill appears once in chips
- UI prevents duplicate (disabled/grayed)
- Template saves with one instance
- No duplicates after save
- Validation works correctly

**Fail:**
- Cannot add skill first time
- Skill can be added twice
- No visual indication of duplicate
- Template saves with duplicates
- Multiple instances after reopening
- No validation for duplicates

**Coverage:** AC 8
