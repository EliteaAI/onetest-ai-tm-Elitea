---
id: ELITEA-1260
title: "End-to-End SharePoint Toolkit Create → Configure → Use"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1260: End-to-End SharePoint Toolkit Create → Configure → Use

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify the complete end-to-end workflow: creating a Delegated SharePoint credential, creating a toolkit using it, assigning the toolkit to an agent, and successfully executing a tool — all in a single uninterrupted flow.

**Coverage:**
- Credential creation with Delegated auth mode and OAuth login
- Toolkit creation with the new credential + tool selection
- Agent assignment of the toolkit
- Tool execution from agent chat
- Complete happy path for the new OAuth feature

## Preconditions

- Logged in as Owner with both credential and toolkit creation permissions
- Azure AD App with delegated permissions ready
- SharePoint site with accessible content
- No pre-existing SharePoint credentials required

## Test Data

- Credential name: `sp-e2e-delegated`
- Toolkit name: `sp-e2e-toolkit`
- Agent name: `sp-e2e-agent` (new or existing)
- OAuth Discovery Endpoint: `https://login.microsoftonline.com/<tenant_id>`
- Scopes: `sites.read.all user.read files.read.all`
- Tools enabled: Get files list, Read document
- Agent prompt: `List all files in the Shared Documents library on SharePoint`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to /credentials → Add Credential → SharePoint | Form opens |
| 2 | Fill: Display Name sp-e2e-delegated, Client Id, Site Url. Select Delegated. Fill Oauth Discovery Endpoint and Scopes | Form complete |
| 3 | Click Login | OAuth popup opens |
| 4 | Complete OAuth authentication | Token stored. Popup closes |
| 5 | Click Test connection | Success |
| 6 | Click Save | Credential sp-e2e-delegated created |
| 7 | Navigate to Toolkits → Create → SharePoint | Toolkit form opens |
| 8 | Fill: Toolkit Name sp-e2e-toolkit. Select sp-e2e-delegated in SharePoint Configuration | Credential attached |
| 9 | Enable Get files list and Read document in TOOLS section | Tools enabled |
| 10 | Click Save | Toolkit sp-e2e-toolkit saved |
| 11 | Navigate to Agents → Create or open an existing agent | Agent editor opens |
| 12 | Assign sp-e2e-toolkit to the agent. Save the agent | Toolkit assigned. Agent saved |
| 13 | Open agent chat. Send: List all files in the Shared Documents library on SharePoint | Agent invokes Get files list. Returns actual SharePoint file listing |
| 14 | Verify the response contains real file names from the SharePoint site | Files match what exists in SharePoint |

## Expected Final State

Files match what exists in SharePoint

## Pass/Fail Criteria

**Pass:**
- All creation steps complete without error
- Toolkit is usable immediately after creation
- Agent returns SharePoint data using the Delegated auth flow
- Complete flow takes no more than 10 minutes (usability)

**Fail:**
- Any step in the flow fails with an error
- Credential/toolkit created but tool execution fails
- Agent does not pick up the new toolkit
- SharePoint data not returned (empty or error response)
