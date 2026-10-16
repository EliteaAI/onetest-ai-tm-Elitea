---
id: ELITEA-3974
title: "Chat Modules menu displays the exact specified labels and tooltip copy for the new modules"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, chat-modules, ui, copy]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3974: Chat Modules menu displays the exact specified labels and tooltip copy for the new modules

## Preconditions

- User is logged in to `{{base_url}}`

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Chat Modules menu | Menu is displayed |
| 2 | Locate the "Skills Builder" entry and read its tooltip | Label reads "Skills Builder"; tooltip describes creating/updating Skills directly from chat |
| 3 | Locate the "Project Context Builder" entry and read its tooltip | Label reads "Project Context Builder"; tooltip describes creating/updating Project Context directly from chat |

## Expected Final State

Both modules display the specified label text and tooltip copy exactly.

## Pass/Fail Criteria

**Pass:**
- Labels and tooltips match the specified copy

**Fail:**
- Labels or tooltip copy are missing, truncated, or inaccurate
