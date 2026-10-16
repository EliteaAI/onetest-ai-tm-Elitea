---
id: ELITEA-3963
title: "Skill creation from chat completes directly when the request already contains all required information"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, skills-builder, happy-path]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3963: Skill creation from chat completes directly when the request already contains all required information

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder is enabled

## Test Data

| Field | Value |
|-------|-------|
| Skill name | Daily Standup Summarizer |
| Description | Summarizes daily standup notes into action items |
| Instructions | Given raw standup notes, extract blockers, decisions, and action items as a bulleted list |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a chat message providing the Skill name, description, and instructions in full | The assistant proceeds to create the Skill without asking clarifying questions |
| 2 | Inspect the created Skill's fields | Name, Description, and Instructions/content match exactly what was provided in the request |
| 3 | Check the chat response | A "Skill: Daily Standup Summarizer" chip/link is shown in the chat response |

## Expected Final State

A fully specified chat request creates a Skill with correctly populated fields and a visible chip/link, with no unnecessary clarification.

## Pass/Fail Criteria

**Pass:**
- Skill created with correct Name/Description/Instructions
- Skill chip/link shown in chat response
- No clarifying question shown when information was already complete

**Fail:**
- Skill not created, created with incorrect/missing fields, or a clarifying question is shown despite complete information
