---
id: ELITEA-4903
title: "Verify switching project updates chat history and Explore content"
priority: critical
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4903: Verify switching project updates chat history and Explore content


## Preconditions

- User is logged in to `{{base_url}}`
- User has two projects (A and B) with different chats

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Projects | Project A; Project B |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select Project A in the project selector | The Chats history shows Project A's chats |
| 2 | Switch to Project B | The Chats history refreshes and shows only Project B's chats and folders |
| 3 | Hover **Explore** and open **Agents** | The Agents page shows Project B's content |
| 4 | Switch back to Project A | The history and the open section page show Project A's content |

## Expected Final State

The sidebar and the section page reflect the selected project.

## Pass/Fail Criteria

**Pass:**
- History and section content always match the selected project

**Fail:**
- Stale chats from the previous project remain, or content from the wrong project is shown
