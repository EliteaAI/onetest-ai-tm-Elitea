---
id: ELITEA-1272
title: "Delegated Auth — SharePoint Tools Execute Using Browser-Session Token"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1272: Delegated Auth — SharePoint Tools Execute Using Browser-Session Token

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that SharePoint tools in an agent run successfully using the in-browser OAuth token obtained via the Delegated auth flow (Graph API execution path).

**Coverage:**
- Agent runtime injects mcp_tokens into toolkit settings
- Token is correctly resolved by oauth_discovery_endpoint key
- SharepointGraphWrapper is instantiated (not SharepointRestWrapper)
- Get files list and Read document tools execute successfully with delegated token
- Microsoft Graph API is used for all operations in Delegated mode

## Preconditions

- A `sp-delegated-oauth` credential exists with a valid token stored in the browser session
- A SharePoint toolkit `sp-delegated-toolkit` is configured using `sp-delegated-oauth`
- The toolkit has Get files list and Read document tools enabled
- A test agent using `sp-delegated-toolkit` is available
- The SharePoint document library contains at least one .docx or .txt file

## Test Data

- Credential: `sp-delegated-oauth`
- Toolkit: `sp-delegated-toolkit`
- Agent prompt 1: `List all files in the SharePoint document library`
- Agent prompt 2: `Read the file named test-file.docx from the SharePoint document library`
- Expected file name: `test-file.docx`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the agent using sp-delegated-toolkit. Open the agent chat | Agent chat interface is shown |
| 2 | Send the prompt: List all files in the SharePoint document library | Agent invokes the Get files list tool. A list of file names from the SharePoint document library is returned — not an error or empty list |
| 3 | Verify in browser DevTools Network tab that the API call was made to https://graph.microsoft.com/v1.0/... | Network request to Microsoft Graph API is visible. No calls to https://<tenant>.sharepoint.com/_api/ (REST API) |
| 4 | Send the prompt: Read the file named test-file.docx | Agent invokes the Read document tool. The document content is returned |
| 5 | Inspect the response — verify no McpAuthorizationRequired or token expired errors | Response contains document content. No auth errors |

## Expected Final State

Response contains document content. No auth errors

## Pass/Fail Criteria

**Pass:**
- Agent tools return actual SharePoint data using the delegated token
- Network calls use graph.microsoft.com endpoint (Delegated/Graph path)
- No McpAuthorizationRequired errors during execution
- Tool responses match actual SharePoint content

**Fail:**
- Tools return empty or error response
- Calls go to SharePoint REST API (_api/) instead of Graph API
- McpAuthorizationRequired is raised even though a valid token exists
- Token not injected into toolkit at runtime
