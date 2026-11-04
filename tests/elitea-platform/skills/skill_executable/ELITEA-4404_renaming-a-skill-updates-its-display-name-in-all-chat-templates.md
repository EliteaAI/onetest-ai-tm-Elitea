---
id: ELITEA-4404
title: "Renaming a skill updates its display name in all chat templates"
priority: critical
type: functional
module: chat-templates/skills
status: ready
execution_type: manual
tags: [user_story:6925, feat:skills, feat:chat-templates, skills-in-templates, cascade-update]
requirements: [EliteaAI/elitea_issues#6925]
---
# ELITEA-4404: Renaming Skill Updates Name in Templates

**Module:** Chat Templates / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that renaming a skill triggers cascade update to all templates, updating the display name while maintaining the same skill reference by ID.

## Preconditions

- Skill "Code Reviewer" exists and is included in a template
- User is logged in as project admin

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Original Skill Name | Code Reviewer |
| New Skill Name | Senior Code Reviewer |
| Template | Any template containing "Code Reviewer" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General → Chat templates | Chat templates page loads |
| 2 | Open a template and verify the skill displays as "Code Reviewer" | Skill chip shows "Code Reviewer" name |
| 3 | Close the template modal | Modal closes |
| 4 | Navigate to Skills section | Skills page loads |
| 5 | Open the skill editor for "Code Reviewer" | Skill editor opens |
| 6 | Rename the skill to "Senior Code Reviewer" and save | Skill renamed and saved successfully |
| 7 | Navigate back to Settings → General → Chat templates | Chat templates page loads |
| 8 | Open the same template editor | Template modal opens |
| 9 | Verify the skill chip now displays "Senior Code Reviewer" | Skill chip shows updated name |
| 10 | Verify the skill icon and position remain unchanged | Icon and position unchanged |

## Expected Final State

- Skill rename triggers cascade update to all templates
- Skill name in template is updated to new name immediately
- Skill icon and chip styling remain unchanged
- Template continues to reference the same skill (by ID, not name)
- Template list also shows updated skill name
- No duplicate entries or broken references appear

## Pass/Fail Criteria

**Pass:**
- Skill renamed successfully
- Template shows new skill name
- Skill icon unchanged
- Template references same skill by ID
- Template list shows updated name
- No duplicates or broken references

**Fail:**
- Skill rename fails
- Template still shows old name
- Skill icon changes incorrectly
- Template loses skill reference
- Template list not updated
- Duplicate or broken references

**Coverage:** AC 7
