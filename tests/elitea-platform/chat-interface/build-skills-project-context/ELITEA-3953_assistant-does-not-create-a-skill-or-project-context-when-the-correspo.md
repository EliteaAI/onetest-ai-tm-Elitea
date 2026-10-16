---
id: ELITEA-3953
title: "Assistant does not create a Skill or Project Context when the corresponding builder module is disabled"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, skills-builder, project-context-builder, negative]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3953: Assistant does not create a Skill or Project Context when the corresponding builder module is disabled

## Preconditions

- User is logged in to `{{base_url}}`

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Chat Modules and ensure Skills Builder and Project Context Builder are both disabled | Both toggles show as off |
| 2 | Send the message: "Create a skill that summarizes daily standup notes" | The assistant does not create a Skill entity and does not show a Skill chip/link in the response |
| 3 | Send the message: "Create project context describing our QA process" | The assistant does not create or update any Project Context entity and does not show a Project Context chip/link |

## Expected Final State

No Skill or Project Context entity is created while the respective builder module is disabled, regardless of how explicit the chat request is.

## Pass/Fail Criteria

**Pass:**
- No Skill entity created with Skills Builder disabled
- No Project Context entity created/updated with Project Context Builder disabled

**Fail:**
- A Skill or Project Context entity is created despite its builder module being disabled
