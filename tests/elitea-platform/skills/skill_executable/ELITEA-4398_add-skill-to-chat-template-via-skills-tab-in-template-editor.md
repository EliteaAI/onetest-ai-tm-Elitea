---
id: ELITEA-4398
title: "Add skill to chat template via Skills tab in template editor"
priority: critical
type: functional
module: chat-templates/skills
status: ready
execution_type: manual
tags: [user_story:6925, feat:skills, feat:chat-templates, skills-in-templates]
requirements: [EliteaAI/elitea_issues#6925]
---
# ELITEA-4398: Add Skill to Chat Template via Skills Tab

**Module:** Chat Templates / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that skills can be successfully added to chat templates through the Skills tab in the template editor, with both project skills and Catalog skills displaying correctly.

## Preconditions

- User is logged in as project admin
- At least one skill exists in the project (e.g., "Code Reviewer")
- At least one published Catalog skill exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Template Name | Template 1 |
| Project Skill | Code Reviewer |
| Catalog Skill | Any published Catalog skill |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click Settings icon (bottom left navigation) | Settings page opens |
| 2 | Click "General" in the Settings sidebar | General settings section displays |
| 3 | Scroll to "Chat templates" section and click "+ Template" button | Create Template modal opens |
| 4 | In the Create Template modal, enter template name "Template 1" | Template name field populated |
| 5 | Click in the "Search participants..." field under PARTICIPANTS section | Tabs appear: Agents, Pipelines, Toolkits, MCPs, Users, Skills |
| 6 | Click the "Skills" tab | Skills tab activates, search field displays |
| 7 | Search for "Code Reviewer" and click on it to add | Skill chip appears in PARTICIPANTS section with skill icon and name |
| 8 | Search for a published Catalog skill and add it | Catalog skill chip appears with "Catalog" badge |
| 9 | Click "Save" to save the template | Template saves successfully |
| 10 | Verify template appears in the list showing "1 of 5" and reopen to confirm skills persist | Skills persist after closing and reopening the template |

## Expected Final State

- Skills tab appears when search field is activated
- Search returns matching skills from own project and published Catalog
- Added skills appear as chips with correct icons and names
- Catalog skills display "Catalog" badge
- Template saves successfully and appears in the list
- Skills persist after save and reopening

## Pass/Fail Criteria

**Pass:**
- Skills tab is visible and functional in template editor
- Search returns skills from both project and Catalog
- Skills appear as chips with correct icons
- Catalog skills show "Catalog" badge
- Template saves with skills included
- Skills persist after page reload

**Fail:**
- Skills tab not available or not functional
- Search does not return expected skills
- Skill chips missing icons or names
- Catalog badge missing
- Template fails to save with skills
- Skills do not persist after reopening

**Coverage:** AC 1, AC 10
