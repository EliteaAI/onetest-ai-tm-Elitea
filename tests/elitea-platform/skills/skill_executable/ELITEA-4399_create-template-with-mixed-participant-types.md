---
id: ELITEA-4399
title: "Create template with mixed participant types (agent, pipeline, toolkit, user, skill)"
priority: critical
type: functional
module: chat-templates/skills
status: ready
execution_type: manual
tags: [user_story:6925, feat:skills, feat:chat-templates, skills-in-templates]
requirements: [EliteaAI/elitea_issues#6925]
---
# ELITEA-4399: Create Template with Mixed Participant Types

**Module:** Chat Templates / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that templates can contain a mix of all participant types (agents, pipelines, toolkits, users, and skills) simultaneously and persist correctly.

## Preconditions

- User is logged in as project admin
- At least one of each entity exists: agent, pipeline, toolkit, user, skill
- Navigate to Settings → General → Chat templates section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings` |
| Template Name | Mixed Participants Template |
| Agent | Any available agent |
| Pipeline | Any available pipeline |
| Toolkit | Any available toolkit |
| User | Any team member |
| Skill | Any available skill |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click "+ Template" button | Create Template modal opens |
| 2 | Enter template name "Mixed Participants Template" and click "Search participants..." field | Template name populated, tabs appear |
| 3 | From the Agents tab, add one agent | Agent chip appears in PARTICIPANTS section |
| 4 | From the Pipelines tab, add one pipeline | Pipeline chip appears in PARTICIPANTS section |
| 5 | From the Toolkits tab, add one toolkit | Toolkit chip appears in PARTICIPANTS section |
| 6 | From the Users tab, add one user | User chip appears in PARTICIPANTS section |
| 7 | From the Skills tab, add one skill | Skill chip appears in PARTICIPANTS section |
| 8 | Verify all 5 participants display as chips in the PARTICIPANTS section | All 5 participants visible with correct icons and names |
| 9 | Click "Save" to save the template | Template saves successfully, counter shows increment (e.g., "1 of 5" → "2 of 5") |
| 10 | Re-open the template and verify all 5 participants are present | All participants persist with correct icons and types |

## Expected Final State

- All participant types can be added through their respective tabs
- Each participant displays with correct icon and name as a chip
- Template saves successfully with mixed participants
- Template counter increments correctly
- All participants persist after save and reopening
- Template list shows correct participant count and icons

## Pass/Fail Criteria

**Pass:**
- All 5 participant types can be added to single template
- Each participant displays with correct icon/name
- Template saves successfully
- Template counter increments
- All participants persist after reopening
- Template list card shows all participant types

**Fail:**
- Cannot add all participant types
- Participant chips missing or incorrect
- Template fails to save
- Counter does not increment
- Participants lost after reopening
- Template list does not show all types

**Coverage:** AC 2, AC 9
