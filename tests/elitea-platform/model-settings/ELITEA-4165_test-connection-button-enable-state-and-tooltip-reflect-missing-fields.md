---
id: ELITEA-4165
title: "Test connection button enable state and tooltip reflect missing required fields, API protocol required only for DIAL"
priority: critical
type: functional
module: model-settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

## Preconditions

- User is logged in to `{{base_url}}` as a project admin.
- Project has at least one non-DIAL and one DIAL credential saved.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Non-DIAL credential | Any saved non-DIAL credential |
| DIAL credential | Any saved DIAL credential |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open form with no fields filled | Test connection disabled. |
| 2 | Hover over disabled button | Tooltip names missing fields (AI Credentials, Model Name). |
| 3 | Select non-DIAL credential + Model Name | Button enabled, no protocol needed. |
| 4 | Select DIAL credential + Model Name, leave protocol unset | Button stays disabled; tooltip names protocol as missing. |
| 5 | Set the protocol | Button becomes enabled. |

## Expected Final State

Button enable state and tooltip correctly reflect missing fields, with protocol required only for DIAL.

## Pass/Fail Criteria

**Pass:**
- Enable/disable and tooltip logic match the above for both credential types.

**Fail:**
- Button state or tooltip is incorrect for any step.
