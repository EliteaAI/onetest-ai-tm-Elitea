---
id: ELITEA-4852
title: "Restore Max Chat Starters per Version to the default of 4"
priority: high
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
known_issues: [elitea_issues#7750]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin
- The current value is noted (restore it at the end)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/admin/app/features#chat_configuration` |
| Value before restore | 7 |
| Default | 4 |
| Restore control | the field's restore-default control (the pattern used on other Guardrails fields) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Chat Configuration → Chat Starters, set the value to 7 and Save | Saved; `platform_settings` returns 7 |
| 2 | Find the restore-default control for "Max Chat Starters per Version" | The control is shown for this field |
| 3 | Use the control | The field is set to 4 |
| 4 | Save, then call `GET {{base_url}}/api/v2/elitea_core/platform_settings/prompt_lib` | `conversation_starters_max` is 4 |
| 5 | Restore the original value | Restored |

## Expected Final State

The admin can get back to the default of 4 without knowing it. The setting is back at its original value.

## Pass/Fail Criteria

**Pass:**
- A restore-default control exists, sets 4, and the saved value is delivered as 4

**Fail:**
- There is no restore-default control, or it sets a value other than 4
