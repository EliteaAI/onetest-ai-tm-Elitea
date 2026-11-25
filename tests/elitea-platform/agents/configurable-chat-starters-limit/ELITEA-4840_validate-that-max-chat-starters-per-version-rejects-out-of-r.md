---
id: ELITEA-4840
title: "Validate that Max Chat Starters per Version rejects out-of-range values and saves 1 and 10"
priority: critical
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
known_issues: [elitea_issues#7747]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin
- The current value of Max Chat Starters per Version is noted (the setting is platform-wide; restore it at the end)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/admin/app/features#chat_configuration` |
| Invalid values | `""` (cleared), `-1`, `4.5`, `0`, `11`, `1e1` |
| Valid boundary values | `1`, `10` |
| Inline error text | "Enter a whole number from 1 to 10" |
| Admin value API | `GET {{base_url}}/api/v2/admin/plugin_config_values/administration/guardrails` → `values.max_conversation_starters` |
| Delivered value API | `GET {{base_url}}/api/v2/elitea_core/platform_settings/prompt_lib` → `conversation_starters_max` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Admin → Features → Chat Configuration and expand the Chat Starters card | The card shows the field "Max Chat Starters per Version" with the current value and the 1–10 help text |
| 2 | For each invalid value in Test Data: enter it in the field | The inline error "Enter a whole number from 1 to 10" is shown and Save is disabled |
| 3 | After the invalid values, call the admin value API | The stored value is unchanged |
| 4 | Enter `1` and click Save | No inline error; "Configuration saved successfully" is shown; no Reload chip appears |
| 5 | Call the delivered value API | `conversation_starters_max` is 1 with no restart |
| 6 | Enter `10` and click Save, then call the delivered value API | Saved successfully; `conversation_starters_max` is 10 |
| 7 | Restore the value noted in the preconditions and Save | The original value is stored and delivered |

## Expected Final State

No invalid value was ever stored. The setting is back at its original value.

## Pass/Fail Criteria

**Pass:**
- Every invalid value shows the inline error and Save stays disabled
- 1 and 10 save and are delivered through `platform_settings` without a restart

**Fail:**
- Any invalid value leaves Save enabled, shows no inline error, or gets stored
- 1 or 10 is rejected, or the delivered value doesn't follow the saved one
