---
id: ELITEA-3365
title: "Chat Modules: Skills Builder and Project Context Builder toggles, default state, and tooltips"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, story:6239, regression, chat-modules, skills-builder, project-context-builder, ui]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3365: Chat Modules: Skills Builder and Project Context Builder toggles, default state, and tooltips

## Objective

Verify that Skills Builder and Project Context Builder appear as independent toggles in the Chat Modules menu, are disabled by default, and display correct labels and tooltips.

## Preconditions

- User is logged in to `{{base_url}}`
- A new conversation is started

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Chat Modules menu | Menu opens listing all modules including "Skills Builder" and "Project Context Builder" |
| 2 | Verify default state of Skills Builder | Skills Builder toggle is OFF (disabled) by default |
| 3 | Verify default state of Project Context Builder | Project Context Builder toggle is OFF (disabled) by default |
| 4 | Hover over Skills Builder to view tooltip | Tooltip displays: describes creating/updating Skills directly from chat |
| 5 | Hover over Project Context Builder to view tooltip | Tooltip displays: describes creating/updating Project Context directly from chat |
| 6 | Enable Skills Builder only | Skills Builder becomes enabled; Project Context Builder remains disabled |
| 7 | Disable Skills Builder, enable Project Context Builder only | Project Context Builder becomes enabled; Skills Builder remains disabled |
| 8 | Enable both modules simultaneously | Both modules show as enabled independently |

## Expected Final State

Both modules are present in Chat Modules menu, disabled by default, independently toggleable, with descriptive tooltips.

## Pass/Fail Criteria

**Pass:**
- Both modules listed in Chat Modules menu
- Both disabled by default in new conversations
- Each module toggles independently of the other
- Tooltips present and accurately describe module purpose
- Labels read "Skills Builder" and "Project Context Builder" exactly

**Fail:**
- Module missing from menu
- Module enabled by default
- Toggles are linked (enabling one affects the other)
- Tooltip missing or inaccurate
