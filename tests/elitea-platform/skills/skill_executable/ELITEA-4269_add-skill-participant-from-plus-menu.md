---
id: ELITEA-4269
title: "Add Skill Participant from Plus Menu"
priority: critical
type: functional
module: chat/skills
status: ready
execution_type: manual
tags: [user_story:6924, feat:skills, feat:chat-participants, skills-as-participants]
requirements: [EliteaAI/elitea_issues#6924]
---
# ELITEA-4269: Add Skill Participant from Plus Menu

**Module:** Chat / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that skills can be successfully added as chat participants from the "+" menu, with both "My skills" and "Catalog" sections displaying correctly, and the skill appearing in the PARTICIPANTS panel with version badge.

## Preconditions

- User is logged into https://next.elitea.ai/app/
- User has at least one skill published in "My skills"
- Catalog has at least one published skill available
- User has created or opened a chat session

## Test Data

| Skill Source | Example Skill | Expected Availability |
|--------------|---------------|----------------------|
| My skills | User's own skill (e.g., "jira-skill") | All versions available |
| Catalog | Public catalog skill (e.g., "animal-joke") | Published versions only |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a chat session on https://next.elitea.ai/app/ | Chat interface loads successfully |
| 2 | Click the "+" button in the chat interface | Dropdown menu appears with "Skills" option visible |
| 3 | Hover over or click "Skills" in the dropdown menu | Submenu expands showing two sections: "My skills" and "Catalog" |
| 4 | Verify "My skills" section lists user's own skills | User's skills are displayed (e.g., "jira-skill", "confluence-artifact-in...") |
| 5 | Verify "Catalog" section lists public catalog skills with "Catalog" badge | Catalog skills are displayed with visible "Catalog" badge (e.g., "animal-joke") |
| 6 | Click a skill from "My skills" (e.g., "jira-skill") | Skill is added to the chat |
| 7 | Verify the skill appears in the PARTICIPANTS panel on the right side | Skill participant appears in PARTICIPANTS panel with name and version badge (e.g., "jira-skill" with "base" version) |
| 8 | Repeat steps 2-7 with a skill from "Catalog" section | Catalog skill is added and appears in PARTICIPANTS panel with version badge |

## Expected Final State

- Both "My skills" and "Catalog" skills can be successfully added as participants
- Skills appear in PARTICIPANTS panel with correct name and version badge
- "+" menu displays skills organized under "My skills" and "Catalog" sections
- Catalog skills show "Catalog" badge in the menu

## Pass/Fail Criteria

**Pass:**
- "+" menu shows "Skills" option
- "Skills" submenu displays "My skills" and "Catalog" sections
- User's own skills appear in "My skills" section
- Catalog skills appear with "Catalog" badge
- Selected skills from both sections are added to PARTICIPANTS panel
- Version badge is displayed for each skill participant

**Fail:**
- "Skills" option not visible in "+" menu
- Submenu does not show both "My skills" and "Catalog" sections
- Skills do not appear in the correct section
- Catalog badge missing or incorrect
- Selected skill does not appear in PARTICIPANTS panel
- Version badge missing or incorrect
