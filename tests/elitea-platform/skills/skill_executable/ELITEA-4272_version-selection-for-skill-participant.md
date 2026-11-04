---
id: ELITEA-4272
title: "Version Selection for Skill Participant"
priority: critical
type: functional
module: chat/skills
status: ready
execution_type: manual
tags: [user_story:6924, feat:skills, feat:chat-participants, skills-as-participants, versioning]
requirements: [EliteaAI/elitea_issues#6924]
---
# ELITEA-4272: Version Selection for Skill Participant

**Module:** Chat / Skills · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that skill participants support version selection per conversation, with different version availability rules: own skills show all versions, Catalog skills show published versions only.

## Preconditions

- User is logged into https://next.elitea.ai/app/
- User has at least one skill with multiple versions (e.g., "jira-skill" with versions "base", "v1", "v2-draft")
- Catalog has at least one skill with multiple published versions
- A chat session is open

## Test Data

| Skill Source | Skill Name | Available Versions | Expected Behavior |
|--------------|------------|-------------------|-------------------|
| My skills | jira-skill | base, v1, v2-draft | All versions (including drafts) should be available |
| Catalog | animal-joke | v1, v2 (published only) | Only published versions should be available |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click "+" menu → Skills → My skills | My skills submenu displays user's skills |
| 2 | Click on a user's own skill with multiple versions (e.g., "jira-skill") | Version selection prompt appears (or skill is added with default version) |
| 3 | Verify that ALL versions are available for selection, including draft versions | Version dropdown shows all versions: "base", "v1", "v2-draft" |
| 4 | Select a specific version (e.g., "v1") | Version "v1" is selected |
| 5 | Confirm the selection | Skill is added to PARTICIPANTS panel with "v1" version badge |
| 6 | Remove the skill participant (if needed for next test) | Skill removed from PARTICIPANTS panel |
| 7 | Click "+" menu → Skills → Catalog | Catalog submenu displays public skills |
| 8 | Click on a Catalog skill with multiple versions (e.g., "animal-joke") | Version selection prompt appears |
| 9 | Verify that ONLY published versions are available for selection (no drafts) | Version dropdown shows only published versions: "v1", "v2" (no draft versions) |
| 10 | Select a published version (e.g., "v2") | Version "v2" is selected |
| 11 | Confirm the selection | Skill is added to PARTICIPANTS panel with "v2" version badge |
| 12 | Verify the selected version is displayed in the PARTICIPANTS panel | Version badge shows correct version ("v1" for own skill, "v2" for catalog skill) |

## Expected Final State

- Own skills (My skills) display all versions including drafts for selection
- Catalog skills display only published versions for selection
- Selected version is applied to the skill participant in the conversation
- Version badge in PARTICIPANTS panel reflects the selected version
- Version selection is per-conversation (different chats can use different versions)

## Pass/Fail Criteria

**Pass:**
- Own skills show all versions (including drafts) in version selector
- Catalog skills show only published versions in version selector
- Selected version is applied to the skill participant
- Version badge in PARTICIPANTS panel displays correct version
- Version selection works independently per conversation

**Fail:**
- Own skills do not show all versions or exclude drafts
- Catalog skills show draft or unpublished versions
- Selected version is not applied or displays incorrectly
- Version badge is missing, incorrect, or does not update
- Version selection affects other conversations incorrectly
