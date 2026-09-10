---
id: ELITEA-2793
title: "Generated Skill and Project Context chips reopen the entity in Canvas mode"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, canvas, skills-builder, project-context-builder]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2793: Generated Skill and Project Context chips reopen the entity in Canvas mode

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder and Project Context Builder are enabled
- Canvas mode is available in the environment

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Skill via chat and locate the resulting chip/link in the chat response | A Skill chip/link is present |
| 2 | Click the Skill chip/link | The Skill opens in Canvas mode showing its correct, current content |
| 3 | Create/update a Project Context via chat and locate the resulting chip/link | A Project Context chip/link is present |
| 4 | Click the Project Context chip/link | The Project Context opens in Canvas mode showing its correct, current content |

## Expected Final State

Both chip types reliably reopen their respective entity in Canvas mode with accurate content.

## Pass/Fail Criteria

**Pass:**
- Skill chip opens the correct Skill in Canvas mode
- Project Context chip opens the correct Project Context in Canvas mode

**Fail:**
- Clicking a chip fails to open Canvas mode, opens the wrong entity, or shows stale/incorrect content
