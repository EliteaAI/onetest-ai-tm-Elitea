---
id: ELITEA-4403
title: "Deleting a skill removes it from all chat templates in affected projects"
priority: critical
type: functional
module: chat-templates/skills
status: ready
execution_type: manual
tags: [user_story:6925, feat:skills, feat:chat-templates, skills-in-templates, cascade-delete]
requirements: [EliteaAI/elitea_issues#6925]
---
# ELITEA-4403: Deleting Skill Removes from All Templates

**Module:** Chat Templates / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that deleting a skill triggers cascade update, removing it from all templates that reference it, while keeping other participants and template validity intact.

## Preconditions

- Skill "Code Reviewer" exists in the project
- Two templates exist (Template A and Template B), both containing "Code Reviewer"
- User is logged in as project admin

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Skill to Delete | Code Reviewer |
| Template A | Contains Code Reviewer + other participants |
| Template B | Contains Code Reviewer + other participants |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General → Chat templates section | Chat templates page loads |
| 2 | Open Template A and verify "Code Reviewer" skill chip is present | Skill chip visible in participants |
| 3 | Close Template A and open Template B, verify "Code Reviewer" skill chip is present | Skill chip visible in participants |
| 4 | Navigate to Skills section | Skills page loads |
| 5 | Delete "Code Reviewer" skill and confirm deletion | Skill deleted, confirmation shown |
| 6 | Navigate back to Settings → General → Chat templates | Chat templates page loads |
| 7 | Open Template A editor | Template A modal opens |
| 8 | Verify "Code Reviewer" skill is NO LONGER present in participants | Skill chip removed, other participants remain |
| 9 | Close and open Template B editor | Template B modal opens |
| 10 | Verify "Code Reviewer" skill is also removed from this template | Skill chip removed, other participants remain |

## Expected Final State

- Skill deletion triggers cascade update across all templates
- Skill is removed from all templates that referenced it
- Templates remain valid and functional after skill removal
- Other participants in templates remain unaffected
- Opening template editors shows updated participant lists
- No errors when opening or editing affected templates

## Pass/Fail Criteria

**Pass:**
- Skill deleted successfully
- Skill removed from Template A
- Skill removed from Template B
- Other participants intact
- Templates remain valid
- No errors opening templates

**Fail:**
- Skill not deleted or error occurs
- Skill still present in Template A
- Skill still present in Template B
- Other participants affected
- Templates become invalid
- Errors when opening templates

**Coverage:** AC 7
