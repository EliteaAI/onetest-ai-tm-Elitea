---
id: ELITEA-4628
title: "ELITEA-4628: Add Skill Participant from Plus Menu (My Skills & Catalog)"
priority: critical
type: regression
module: chat/skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, feat:chat-participants, skills-as-participants]
requirements: [EliteaAI/elitea_issues#6924]
---
# ELITEA-4628: Add Skill Participant from Plus Menu (My Skills & Catalog)

**Module:** Chat / Skills · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that skills can be successfully added as chat participants from the "+" menu, with both "My skills" and "Catalog" sections displaying correctly, and skills appearing in the PARTICIPANTS panel with version badges.

**Coverage:**
- Plus menu shows Skills option
- My skills section displays user's own skills
- Catalog section displays public skills with badge
- Skill added to PARTICIPANTS panel with version
- Version badge displays correctly

## Preconditions

- User is logged into {{base_url}}
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
|---|--------|-----------------|
| 1 | Open a chat session on {{base_url}} | Chat interface loads successfully |
| 2 | Click the "+" button in the chat interface | Dropdown menu appears with "Skills" option visible |
| 3 | Hover over or click "Skills" in the dropdown menu | Submenu expands showing two sections: "My skills" and "Catalog" |
| 4 | Verify "My skills" section lists user's own skills | User's skills are displayed (e.g., "jira-skill") |
| 5 | Verify "Catalog" section lists public catalog skills with "Catalog" badge | Catalog skills are displayed with visible "Catalog" badge (e.g., "animal-joke") |
| 6 | Click a skill from "My skills" | Skill is added to the chat |
| 7 | Verify the skill appears in the PARTICIPANTS panel on the right side | Skill participant appears in PARTICIPANTS panel with name and version badge (e.g., "jira-skill" with "base" version) |
| 8 | Click the "+" button again and select a skill from "Catalog" section | Catalog skill is added to chat |
| 9 | Verify Catalog skill appears in PARTICIPANTS panel with version badge | Catalog skill appears with version badge and "Catalog" indicator |

## Expected Final State

- Both "My skills" and "Catalog" skills can be successfully added as participants
- Skills appear in PARTICIPANTS panel with correct name and version badge
- "+" menu displays skills organized under "My skills" and "Catalog" sections
- Catalog skills show "Catalog" badge in both menu and participants panel

## Pass/Fail Criteria

**Pass:**
- Skills from both sources can be added successfully
- PARTICIPANTS panel shows all added skills with version badges
- "+" menu displays correct skill organization and badges

**Fail:**
- "+" menu doesn't show Skills option
- My skills or Catalog section is missing or empty
- Skills don't appear in PARTICIPANTS panel after adding
- Version badges are missing or incorrect

## Notes

**Source functional tests:** ELITEA-4269
**Regression rationale:** Critical UI workflow for adding skills to chat; covers both user-owned and catalog skill sources.
**Selected checkpoints:** Menu navigation, skill addition from both sources, participant panel display with versions.
