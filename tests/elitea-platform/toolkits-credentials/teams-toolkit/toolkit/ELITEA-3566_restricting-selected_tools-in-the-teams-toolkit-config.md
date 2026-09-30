---
id: ELITEA-3566
title: "Restricting selected_tools in the Teams Toolkit Configuration Limits What Is Exposed to Agents/Pipelines"
priority: high
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3566: Restricting selected_tools in the Teams Toolkit Configuration Limits What Is Exposed to Agents/Pipelines

**Module:** Teams Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that configuring a subset of `selected_tools` for the Teams toolkit restricts the tools available at execution time, and that leaving it empty exposes all 7 tools.

## Preconditions

- A Teams toolkit instance linked to an authorized credential, attachable to an Agent or Pipeline

## Test Data

| Variant | selected_tools | Expected |
|---|---|---|
| A | empty | All 7 tools available: `list_teams`, `list_channels`, `list_chats`, `find_chat_messages`, `search_teams_messages`, `send_chat_message`, `send_channel_message` |
| B | 1–2 tools | Only those tools exposed; the rest not selectable/callable |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Teams toolkit instance per Variant A and attach it to an Agent/Pipeline | All 7 tools are available to the Agent/Pipeline |
| 2 | Reconfigure the same toolkit instance per Variant B | Only the selected 1–2 tools are exposed; the rest are not selectable or callable |

## Expected Final State

The set of tools exposed to the Agent/Pipeline always exactly matches the configured `selected_tools`.

## Pass/Fail Criteria

**Pass:**
- Empty selection exposes all 7 tools; a restricted selection exposes only the chosen tools

**Fail:**
- Any tool outside the configured selection remains callable, or a selected tool is missing
