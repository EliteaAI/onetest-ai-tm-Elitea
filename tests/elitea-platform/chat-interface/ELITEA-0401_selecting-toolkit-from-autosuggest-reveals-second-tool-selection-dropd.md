---
id: ELITEA-0401
title: "Selecting Toolkit from `/` Autosuggest Reveals Second Tool Selection Dropdown"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0401: Selecting Toolkit from `/` Autosuggest Reveals Second Tool Selection Dropdown

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that after selecting a Toolkit from the first autosuggest, a second dropdown listing that toolkit's available tools is presented.

**Coverage:**
- First dropdown: Toolkit/MCP selection
- Second dropdown: tool list specific to selected Toolkit

## Preconditions

- Artifacts toolkit in Participants (known to have tools: create_file, upload_file, search_index, list_files, etc.)

## Test Data

- Toolkit: Artifacts
- Expected tools in second dropdown: at minimum create_file, upload_file, search_index

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a new chat conversation with Artifacts in Participants. | Artifacts shown in Participants panel. |
| 2 | Click the chat input, type /. | First autosuggest dropdown appears with Artifacts. |
| 3 | Click Artifacts in the dropdown. | First dropdown closes. Second dropdown appears. |
| 4 | Inspect the second dropdown. | It lists tools belonging to the Artifacts toolkit. |
| 5 | Verify tools match the Artifacts toolkit's known tool set. | Tool names from the Artifacts toolkit are shown. |

## Expected Final State

Tool names from the Artifacts toolkit are shown.

## Pass/Fail Criteria

**Pass:**
- Second dropdown appears after Toolkit selection
- Second dropdown lists tools specific to the selected Toolkit

**Fail:**
- No second dropdown appears
- Second dropdown shows tools from the wrong toolkit
