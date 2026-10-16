---
id: ELITEA-4100
title: "[EliteaAI/elitea_issues#5889] ADO Toolkit: process_images Parameter Configuration"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5889, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend]
requirements: [EliteaAI/elitea_issues#5889]
---

# ELITEA-4100: ADO Toolkit — process_images Parameter Configuration

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the `process_images` parameter is available in ADO toolkit get_comments configuration with correct default value and is properly read from config.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- User can access Agents, Pipelines, or Chat with toolkit integration
- ADO toolkit is available and configured
- ADO credentials configured in toolkit instance

## Test Data

| Parameter | Value |
|-----------|-------|
| `process_images` default | false |
| Config format | JSON/YAML |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkit configuration for ADO board toolkit. | Toolkit config interface loads; editable fields visible. |
| 2 | Locate the `process_images` parameter in get_comments configuration. | Parameter field is present and accessible. |
| 3 | Observe default value when parameter is not explicitly set. | Default value is `false`. |
| 4 | Set `process_images: false` in config; save configuration. | Configuration saved successfully; parameter accepted in config JSON. |
| 5 | Set `process_images: true` in config; save configuration. | Configuration saved successfully; parameter toggled correctly. |
| 6 | Use get_comments tool with `process_images: false`. | Tool instance reads parameter correctly; images not processed. |
| 7 | Use get_comments tool with `process_images: true`. | Tool instance reads parameter correctly; images processed (if present). |
| 8 | Verify parameter persists across multiple tool invocations. | Parameter value remains consistent across calls without re-configuration. |

## Expected Final State

- `process_images` parameter available in ADO get_comments configuration
- Default value is `false`
- Parameter correctly read from config by tool instance
- Parameter persists across invocations
- Valid values: `true`, `false`

## Pass/Fail Criteria

**Pass:** Parameter available with default false; correctly read from config; persists across calls.  
**Fail:** Parameter missing; incorrect default; not persisted; tool rejects valid values.
