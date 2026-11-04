---
id: ELITEA-4406
title: "Template list cards and editor display skill icons and names consistently"
priority: critical
type: functional
module: chat-templates/skills
status: ready
execution_type: manual
tags: [user_story:6925, feat:skills, feat:chat-templates, skills-in-templates, ui-consistency]
requirements: [EliteaAI/elitea_issues#6925]
---
# ELITEA-4406: Template List and Editor Show Skill Icons Correctly

**Module:** Chat Templates / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that skill icons and names display consistently in both template list cards and the template editor, with Catalog badges appearing where applicable.

## Preconditions

- Template 1 exists with "Code Reviewer" skill (project skill)
- Template 2 exists with "Release Notes Generator" (Catalog skill)
- User is logged in as project admin

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Template 1 | Contains project skill "Code Reviewer" |
| Template 2 | Contains Catalog skill "Release Notes Generator" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General → Chat templates section | Chat templates page loads with template list |
| 2 | In the template list, locate Template 1 | Template 1 card visible |
| 3 | Verify the template shows the skill icon (correct entity type icon) | Skill icon displays correctly (skill entity type) |
| 4 | Verify the skill name "Code Reviewer" is visible in the template card | Skill name "Code Reviewer" readable |
| 5 | Locate Template 2 in the list | Template 2 card visible |
| 6 | Verify the Catalog skill shows skill icon and "Catalog" badge | Skill icon and "Catalog" badge visible |
| 7 | Click to open Template 1 editor | Template 1 modal opens |
| 8 | Verify skill chip shows correct icon and name | Skill chip displays matching icon and name |
| 9 | Close and click to open Template 2 editor | Template 2 modal opens |
| 10 | Verify Catalog skill chip shows icon, name, and "Catalog" badge | Skill chip displays icon, name, and badge |

## Expected Final State

- Template list displays skill icons correctly (skill entity type, not agent/toolkit)
- Skill names are visible and readable in template list
- Template editor modal shows consistent skill icons in participant chips
- Catalog skills display "Catalog" badge in both list and editor
- Icons are visually distinct from agent/toolkit/pipeline icons
- Visual consistency between list view and modal editor view

## Pass/Fail Criteria

**Pass:**
- Skill icons correct in template list
- Skill names visible in list
- Template editor shows consistent icons
- Catalog badge displays correctly
- Icons distinct from other types
- Visual consistency maintained

**Fail:**
- Skill icons incorrect or missing in list
- Skill names not visible
- Editor icons inconsistent with list
- Catalog badge missing
- Icons confused with other types
- Visual inconsistency between views

**Coverage:** AC 10
