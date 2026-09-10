---
id: ELITEA-2780
title: "Assistant does not hang when Ask User is disabled and required Skill/Project Context information is missing"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, ask-user, skills-builder, project-context-builder]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2780: Assistant does not hang when Ask User is disabled and required Skill/Project Context information is missing

## Preconditions

- User is logged in to `{{base_url}}`

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enable Skills Builder, disable Ask User, and send an ambiguous request: "Create a skill for onboarding" | The conversation does not hang or show a stuck loading state; the assistant either asks for missing details in a normal chat message or explains it cannot safely proceed |
| 2 | Enable Project Context Builder, disable Ask User, and send an ambiguous request: "Create project context for this" | Same behavior as the previous step: no hang, and either an in-line request for details or a clear explanation is shown |

## Expected Final State

With Ask User disabled, the assistant never silently guesses required fields and never leaves the conversation in a stuck/pending state waiting on a clarification control that cannot appear.

## Pass/Fail Criteria

**Pass:**
- No hang or stuck loading indicator in either scenario
- Assistant responds with either a normal-message request for details or a clear explanation

**Fail:**
- Conversation hangs waiting for a clarification UI that never renders
- Assistant silently creates the entity using guessed values instead of asking or explaining
