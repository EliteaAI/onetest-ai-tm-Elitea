---
id: ELITEA-2693
title: "MCP Toggle Preserves Existing Toolkit State"
priority: high
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, mcp, toggle, migration, regression]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
  - ELITEA-2541
---
# ELITEA-2693: MCP Toggle Preserves Existing Toolkit State

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Re-validate that toolkits previously using "Make tools available by MCP" checkbox retain their MCP access setting with the new toggle. (Re-validation of ELITEA-2541)

**Coverage:**
- Existing MCP-enabled toolkits have toggle in ON state after migration
- Toggle state persists correctly after save
- MCP functionality works correctly with the new toggle
- No regression in MCP access behavior

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- A toolkit exists that had "Make tools available by MCP" enabled before the feature deployment
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Identify a toolkit that had "Make tools available by MCP" enabled before the feature deployment. | Toolkit with legacy MCP enabled is identified. |
| 2 | Open the toolkit configuration and navigate to Tools section. | Tools section displays. |
| 3 | Scroll to MCP toggle at the bottom and verify its state. | Toggle "Enable MCP access for selected tools" is in **ON** position (migrated state preserved). |
| 4 | Toggle it **OFF** and save the toolkit. | Save completes successfully. |
| 5 | Close and reopen the toolkit. | Toolkit reopens. |
| 6 | Verify toggle state. | Toggle is in **OFF** position (state persisted). |
| 7 | Toggle it **ON** and save the toolkit. | Save completes successfully. |
| 8 | Close and reopen the toolkit. | Toolkit reopens. |
| 9 | Verify toggle state. | Toggle is in **ON** position (state persisted). |
| 10 | Connect to the toolkit via MCP and verify selected tools are accessible. | MCP connection succeeds, selected tools are listed. |
| 11 | Execute a tool via MCP connection. | Tool execution **succeeds** with correct results. |

## Expected Final State

MCP toggle is ON, MCP functionality works correctly.

## Pass/Fail Criteria

**Pass:**
- Existing MCP-enabled toolkits have toggle in ON state after migration
- Toggle state persists correctly after save (both ON and OFF)
- MCP functionality works correctly with the new toggle
- No regression in MCP access behavior

**Fail:**
- Existing MCP-enabled toolkits have toggle in OFF state (migration failed)
- Toggle state does not persist after save
- MCP functionality is broken with the new toggle
- Tools are not accessible via MCP when toggle is ON
