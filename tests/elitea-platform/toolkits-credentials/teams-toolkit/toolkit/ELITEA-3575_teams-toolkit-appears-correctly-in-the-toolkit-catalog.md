---
id: ELITEA-3575
title: "Teams Toolkit Appears Correctly in the Toolkit Catalog"
priority: medium
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3575: Teams Toolkit Appears Correctly in the Toolkit Catalog

**Module:** Teams Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Teams toolkit is listed in the toolkit catalog/selection UI with correct name, description, and all 7 tools enumerated before any credential is configured.

## Preconditions

- Access to the toolkit catalog/selection UI (e.g. when adding a toolkit to an Agent or Pipeline)
- No Teams credential needs to be configured yet for this check

## Test Data

- N/A (visual/listing check)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the toolkit catalog/selection UI | Teams toolkit is listed with a recognizable name and description |
| 2 | Open the Teams toolkit's detail/configuration view without configuring a credential | All 7 tools are enumerated: `list_teams`, `list_channels`, `list_chats`, `find_chat_messages`, `search_teams_messages`, `send_chat_message`, `send_channel_message` |

## Expected Final State

The catalog entry and detail view for the Teams toolkit are accurate and complete, independent of credential configuration state.

## Pass/Fail Criteria

**Pass:**
- Toolkit is listed with correct name/description and all 7 tools appear in the detail view

**Fail:**
- Toolkit is missing from the catalog, has an incorrect name/description, or is missing any of the 7 tools in the detail view
