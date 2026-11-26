---
id: ELITEA-4900
title: "Verify + New chat creates only a chat in the selected project"
priority: critical
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4900: Verify + New chat creates only a chat in the selected project


## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a private project and a team project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Projects | Private project; Team project |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select the private project in the project selector | The private project is active |
| 2 | Check the **+ New chat** button | It is a single button with no split/dropdown arrow and no list of other entity types (agents, pipelines and so on) |
| 3 | Open an existing chat, then click **+ New chat** | A new empty chat opens in the selected project |
| 4 | Send a message in the new chat | The chat appears in the sidebar Chats history for the selected project |
| 5 | Repeat steps 1–4 with the team project | The new chat is created in the team project, and not in the private project |

## Expected Final State

One new chat exists in each tested project.

## Pass/Fail Criteria

**Pass:**
- + New chat offers only chat creation, and the chat lands in the selected project

**Fail:**
- Other entity types are offered
- The chat is created in a different project
