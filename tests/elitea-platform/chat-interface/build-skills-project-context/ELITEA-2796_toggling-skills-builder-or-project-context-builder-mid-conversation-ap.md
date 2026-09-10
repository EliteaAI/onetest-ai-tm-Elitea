---
id: ELITEA-2796
title: "Toggling Skills Builder or Project Context Builder mid-conversation applies going forward without affecting prior messages"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, chat-modules, toggle-behavior]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2796: Toggling Skills Builder or Project Context Builder mid-conversation applies going forward without affecting prior messages

## Preconditions

- User is logged in to `{{base_url}}`

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | With Skills Builder disabled, send a Skill creation request | No Skill is created |
| 2 | Enable Skills Builder mid-conversation | Toggle updates to enabled |
| 3 | Re-send the same (or a new) Skill creation request | The Skill is now created successfully |
| 4 | Scroll back to the earlier request sent while the module was disabled | That earlier message/response is unchanged; no retroactive Skill creation occurs for it |

## Expected Final State

Module toggles apply only to requests made after the toggle change; no retroactive effect on prior messages.

## Pass/Fail Criteria

**Pass:**
- Request before enabling produces no Skill
- Request after enabling produces a Skill
- Earlier message remains unchanged

**Fail:**
- Toggling retroactively creates a Skill for the earlier request, or the module change does not take effect for the new request
