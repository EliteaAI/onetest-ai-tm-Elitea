---
id: ELITEA-3370
title: "Skills Builder and Project Context Builder disabled prevents entity creation"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, story:6239, regression, skills-builder, project-context-builder, negative]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3370: Skills Builder and Project Context Builder disabled prevents entity creation

## Objective

Verify that when Skills Builder or Project Context Builder modules are disabled, the assistant does not create the corresponding entity regardless of how explicit the chat request is.

## Preconditions

- User is logged in to `{{base_url}}`
- A conversation is open

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Chat Modules and ensure Skills Builder is disabled | Skills Builder toggle shows as OFF |
| 2 | Ensure Project Context Builder is also disabled | Project Context Builder toggle shows as OFF |
| 3 | Send the message: "Create a skill that summarizes daily standup notes" | The assistant does NOT create a Skill entity; no Skill chip/link appears in the response |
| 4 | Verify no Skill was created | Navigate to Skills list; no new Skill matching the request exists |
| 5 | Send the message: "Create project context describing our QA process" | The assistant does NOT create or update any Project Context entity; no Project Context chip/link appears |
| 6 | Verify no Project Context was created | Navigate to Project Context; no new Project Context matching the request exists |
| 7 | Enable Skills Builder mid-conversation | Toggle updates to enabled |
| 8 | Re-send the Skill creation request | The Skill is now created successfully with a chip/link shown |
| 9 | Scroll back to the earlier request (sent while module was disabled) | That earlier message/response remains unchanged; no retroactive Skill creation |

## Expected Final State

No Skill or Project Context entity is created while the respective builder module is disabled. Enabling the module mid-conversation only affects new requests, not prior messages.

## Pass/Fail Criteria

**Pass:**
- No Skill entity created with Skills Builder disabled
- No Project Context entity created with Project Context Builder disabled
- No chips/links for either entity while modules are disabled
- After enabling module, new request creates entity successfully
- Module toggle does not retroactively affect prior messages

**Fail:**
- Skill or Project Context entity is created despite module being disabled
- Chip/link appears while module is disabled
- Toggling module retroactively creates entity for earlier request
