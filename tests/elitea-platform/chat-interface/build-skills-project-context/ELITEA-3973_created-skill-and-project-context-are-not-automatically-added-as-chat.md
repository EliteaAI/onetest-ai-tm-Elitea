---
id: ELITEA-3973
title: "Created Skill and Project Context are not automatically added as chat participants"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, skills-builder, project-context-builder, participants]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3973: Created Skill and Project Context are not automatically added as chat participants

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder and Project Context Builder are enabled

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Skill via chat | Skill is created successfully |
| 2 | Open the conversation's participant list | The newly created Skill does not appear as a participant |
| 3 | Create/update a Project Context via chat | Project Context is created/updated successfully |
| 4 | Open the conversation's participant list again | The Project Context does not appear as a participant |

## Expected Final State

Neither a newly created Skill nor a newly created/updated Project Context is auto-added as a chat participant.

## Pass/Fail Criteria

**Pass:**
- Skill not listed as a participant after creation
- Project Context not listed as a participant after creation/update

**Fail:**
- Either entity is auto-added to the conversation's participant list
