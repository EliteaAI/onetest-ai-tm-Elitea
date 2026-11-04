---
id: ELITEA-4274
title: "Duplicate Prevention - Single Skill Instance Per Chat"
priority: critical
type: functional
module: chat/skills
status: ready
execution_type: manual
tags: [user_story:6924, feat:skills, feat:chat-participants, skills-as-participants, duplicate-prevention]
requirements: [EliteaAI/elitea_issues#6924]
---
# ELITEA-4274: Duplicate Prevention - Single Skill Instance Per Chat

**Module:** Chat / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that duplicate prevention is enforced, allowing only one instance of each skill per chat, and attempting to add the same skill again is blocked or disabled.

## Preconditions

- User is logged into https://next.elitea.ai/app/
- A chat session is open
- At least one skill is available for adding (e.g., "jira-skill")
- No skill participants are currently in the chat (or test with a fresh chat)

## Test Data

| Skill to Test | Expected Behavior |
|---------------|-------------------|
| jira-skill | First add succeeds, second add is blocked/disabled |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a chat session (new or existing without skill participants) | Chat interface loads successfully |
| 2 | Click "+" menu → Skills → My skills (or Catalog) | Skills submenu displays available skills |
| 3 | Add a skill participant (e.g., "jira-skill") to the chat | Skill is added to PARTICIPANTS panel with version badge |
| 4 | Verify the skill appears in the PARTICIPANTS panel | "jira-skill" is visible in PARTICIPANTS panel |
| 5 | Click "+" menu → Skills → My skills (or Catalog) again | Skills submenu displays available skills |
| 6 | Locate the same skill (e.g., "jira-skill") in the submenu | Skill is visible in the menu |
| 7 | Verify the skill is visually disabled, grayed out, or has an indicator showing it's already added | Skill appears disabled, grayed out, or marked as "Already added" |
| 8 | Attempt to click the already-added skill in the menu | Click is prevented, no action occurs, OR a message indicates the skill is already added |
| 9 | Verify only ONE instance of the skill is present in the PARTICIPANTS panel (no duplicate added) | PARTICIPANTS panel still shows only one instance of "jira-skill" |
| 10 | Send a message to the skill participant to verify functionality is not affected | Skill responds normally, functionality is not impacted by the duplicate prevention check |
| 11 | Remove the skill participant from the PARTICIPANTS panel | Skill is removed successfully |
| 12 | Click "+" menu → Skills and attempt to add the same skill again | Skill can now be added again (no longer disabled), showing that duplicate prevention is per-active-participants |

## Expected Final State

- Only one instance of each skill is allowed per chat
- Attempting to add a duplicate skill is blocked or disabled in the UI
- Duplicate prevention is enforced by disabling the skill in the "+" menu or preventing the add action
- After removal, the skill can be added again (duplicate prevention resets)

## Pass/Fail Criteria

**Pass:**
- First add of skill succeeds, skill appears in PARTICIPANTS panel
- Attempting to add the same skill again is blocked or disabled (grayed out, marked as added, or click prevented)
- No duplicate instance is added to PARTICIPANTS panel
- Only one instance of the skill exists per chat
- After removal, skill can be added again

**Fail:**
- Duplicate skill is added to PARTICIPANTS panel (two or more instances of the same skill)
- Skill is not disabled or marked in the "+" menu when already added
- Duplicate prevention does not work (skill can be added multiple times)
- After removal, skill cannot be added again (duplicate prevention persists incorrectly)
