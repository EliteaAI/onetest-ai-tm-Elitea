---
id: ELITEA-3961
title: "Skills Builder and Project Context Builder appear as independent toggles, disabled by default, with correct tooltips"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, chat-modules, ui]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3961: Skills Builder and Project Context Builder appear as independent toggles, disabled by default, with correct tooltips

## Preconditions

- A brand-new conversation is started

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Chat Modules menu | Menu opens listing Agent & Pipeline Builder, Ask User, Image Creation, Data Analysis, Planner, Python Sandbox, Swarm Mode, Smart Tools Selection, Skills Builder, and Project Context Builder |
| 2 | Inspect the default state of Skills Builder and Project Context Builder | Both are disabled by default |
| 3 | Enable only Skills Builder | Skills Builder becomes enabled while Project Context Builder remains disabled |
| 4 | Disable Skills Builder and enable only Project Context Builder | Project Context Builder becomes enabled while Skills Builder remains disabled, confirming independent toggling |
| 5 | Hover/inspect the tooltip for each new module | Skills Builder tooltip reads to the effect of "Create and update Skills directly from chat."; Project Context Builder tooltip reads to the effect of "Create and update Project Context directly from chat." |

## Expected Final State

Both new modules are present, off by default, independently toggleable, and carry descriptive tooltips.

## Pass/Fail Criteria

**Pass:**
- Both modules listed and disabled by default
- Modules toggle independently of each other
- Tooltips present and describe each module's purpose

**Fail:**
- A module is missing, enabled by default, tied to the other module's toggle, or missing its tooltip
