---
id: ELITEA-1220
title: "SharePoint Toolkit — Agent with /teams/ Site Path Executes SharePoint Operations via Chat"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1220: SharePoint Toolkit — Agent with /teams/ Site Path Executes SharePoint Operations via Chat

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that an Agent using a SharePoint toolkit configured with Site Path teams/TestTeam successfully retrieves data from the /teams/ space when invoked via Chat. Covers: Agent-toolkit integration with /teams/ Site Path; Chat invokes the tool from natural language prompt; response contains /teams/ data; no tool errors in chat response.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- SharePoint toolkit with Site Path teams/TestTeam, Get files list tool enabled
- An Agent configured with that toolkit attached
- /teams/TestTeam site is accessible and contains at least one file

## Test Data

Site Path: teams/TestTeam
Chat prompt: "List the files available in the SharePoint teams site."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents and open the Agent with the SharePoint toolkit attached. Verify toolkit uses Site Path teams/TestTeam. | Agent detail page loads. Toolkit shown in configuration. |
| 2 | Open the Agent in Chat. Send prompt: 'List the files available in the SharePoint teams site.' | Agent processes the prompt and automatically invokes the SharePoint Get files list tool. |
| 3 | Wait for the response. | Chat response contains a file list from the /teams/TestTeam site. No 'tool error', no 'site not found', no HTTP error visible in the response. |

## Expected Final State

Chat response contains a file list from the /teams/TestTeam site. No 'tool error', no 'site not found', no HTTP error visible in the response.

## Pass/Fail Criteria

Pass:
- Agent invokes the SharePoint tool automatically
- Response contains file data from the /teams/ space
- No error messages or wrong-site references in the response

Fail:
- Agent does not invoke the tool or returns a fallback response
- Response contains an error referencing an incorrect site
- Chat response is empty or shows 'site not found'
