---
id: ELITEA-1264
title: "OneNote Tools Require Delegated Auth and Execute Correctly"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1264: OneNote Tools Require Delegated Auth and Execute Correctly

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that OneNote-related tools are available in the SharePoint toolkit and require Delegated auth mode to execute successfully.

**Coverage:**
- OneNote tools are listed in the TOOLS section of the SharePoint toolkit
- OneNote tools require Graph API (Delegated mode)
- At least one OneNote tool (Read OneNote notebook or Get OneNote sections) returns data
- OneNote tools fail or show auth error with App-only credentials (expected behavior)

## Preconditions

- A sp-delegated-oauth credential with a valid browser token and Notes.ReadWrite.All scope
- A SharePoint toolkit with OneNote tools enabled
- An agent using this toolkit
- A OneNote notebook exists in the SharePoint site

## Test Data

- Required scopes for OneNote: add `notes.read.all` to scopes
- Agent prompt: `List all OneNote notebooks in SharePoint`
- Agent prompt 2: `Read the sections of the notebook named Meeting Notes`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to `https://dev.elitea.ai/app/toolkits/create/sharepoint?viewMode=owner` | Toolkit creation form |
| 2 | Scroll to the TOOLS section. Locate OneNote-related tools | OneNote tools visible: Create OneNote page, Get OneNote notebooks, Get OneNote sections, Read OneNote notebook, Read OneNote page sections |
| 3 | Enable a Delegated toolkit (sp-delegated-oauth) and enable Get OneNote notebooks tool. Save toolkit | Toolkit saved |
| 4 | Open the agent using this toolkit. Send: List all OneNote notebooks in my SharePoint site | Agent invokes OneNote tool. Returns notebook list |
| 5 | Enable Get OneNote sections. Send: Read sections of the Meeting Notes notebook | Sections of the notebook are returned |
| 6 | Create an App-only toolkit (no token, no OAuth). Try invoking OneNote tools | OneNote tools return an error about missing delegated auth or the App-only mode does not support OneNote operations |

## Expected Final State

OneNote tools return an error about missing delegated auth or the App-only mode does not support OneNote operations

## Pass/Fail Criteria

**Pass:**
- OneNote tools are visible and toggleable in toolkit TOOLS section
- With Delegated auth + Notes.Read.All scope, OneNote tools return actual notebook data
- Graph API onenote endpoint is called
- Without delegated OAuth, OneNote tools return a meaningful auth/unsupported error

**Fail:**
- OneNote tools are absent from the toolkit configuration
- OneNote tools always fail even with Delegated auth and correct scopes
- App-only mode silently claims success for OneNote operations
