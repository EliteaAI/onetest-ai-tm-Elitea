---
id: ELITEA-4628
title: "ELITEA-4628: Add Skill Participant from Plus Menu in Chat"
priority: critical
type: regression
module: chat/skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, feat:chat-participants, skills-as-participants]
requirements: [EliteaAI/elitea_issues#6924]
---
# ELITEA-4628: Add Skill Participant from Plus Menu in Chat

**Module:** Chat / Skills · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that skills can be successfully added as chat participants from the "+" menu, including both user's own skills and catalog skills, and that they appear correctly in the PARTICIPANTS panel with version badges.

**Coverage:**
- Plus menu displays Skills option with searchable dropdown
- User can search and select skills from the list
- Both "My skills" and "Catalog" skills are available in the dropdown
- Skills added as participants appear in PARTICIPANTS → SKILLS section
- Catalog skills display "Catalog" badge
- Version badges display correctly

## Preconditions

- User is logged into {{base_url}}
- User has at least one own skill available (e.g., "jira-skill")
- Catalog has at least one published skill available (e.g., "code-reviewer")
- User has created or opened a chat session

## Test Data

| Skill Type | Example Skill | Expected Badge |
|------------|---------------|----------------|
| User's own skill | jira-skill | Version badge (e.g., "v1.0") |
| Catalog skill | code-reviewer | "Catalog" + version badge |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a chat session on {{base_url}} | Chat interface loads successfully |
| 2 | Click the "+" button in the chat interface | Dropdown menu appears showing options: Attach Files, Modules, Agents, Pipelines, Skills, Toolkits, MCPs, Invite Users |
| 3 | Click on "Skills" option | Submenu opens with search field "Search skills..." and list of available skills |
| 4 | Observe the skills list | Both user's own skills (e.g., "code-task-breakdown") and catalog skills (e.g., "code-reviewer", "bug-report-generator") appear in the list |
| 5 | Identify catalog skills in the list | Catalog skills display "Catalog" badge next to their names |
| 6 | Click on a user's own skill (e.g., "code-task-breakdown") | Skill is selected |
| 7 | Verify skill appears in PARTICIPANTS panel | In the right panel under PARTICIPANTS → SKILLS section, the skill appears with name and version badge |
| 8 | Click "+" button again and select Skills | Skills menu opens again |
| 9 | Click on a catalog skill (e.g., "code-reviewer" with "Catalog" badge) | Catalog skill is selected |
| 10 | Verify catalog skill appears in PARTICIPANTS panel | In PARTICIPANTS → SKILLS section, catalog skill appears with name, "Catalog" badge, and version (e.g., "code-r... Catalog v1.0") |
| 11 | Verify both skills are listed in PARTICIPANTS → SKILLS | Both user's own skill and catalog skill are visible in the SKILLS section with their respective badges |

## Expected Final State

- Both user's own skills and catalog skills can be added as participants via "+" menu
- Skills appear in PARTICIPANTS panel under SKILLS section
- Catalog skills display "Catalog" badge in both dropdown menu and PARTICIPANTS panel
- Version badges display correctly for all skills
- Chat is ready to interact with added skill participants

## Pass/Fail Criteria

**Pass:**
- "+" menu displays Skills option with searchable dropdown
- Both user's own skills and catalog skills appear in the list
- Catalog skills show "Catalog" badge in dropdown
- Selected skills appear in PARTICIPANTS → SKILLS section
- Catalog badge and version badges display correctly in PARTICIPANTS panel
- Multiple skills can be added to the same chat

**Fail:**
- Skills option missing from "+" menu
- Skills list doesn't show available skills
- Catalog badge missing on catalog skills
- Skills don't appear in PARTICIPANTS panel after selection
- Version or catalog badges missing or incorrect

## Notes

**Source functional tests:** ELITEA-4269
**Regression rationale:** Critical UI workflow for adding skills to chat via + menu; validates skill discovery, selection, and participant display for both user-owned and catalog skills.
**Selected checkpoints:** Menu navigation, skill search/selection, participant panel display with badges for both skill types.
