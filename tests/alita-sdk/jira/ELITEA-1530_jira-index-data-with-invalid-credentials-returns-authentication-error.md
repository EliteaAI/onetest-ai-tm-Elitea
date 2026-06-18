---
id: ELITEA-1530
title: "Jira index_data with invalid credentials returns authentication error instead of misleading success"
priority: high
type: functional
module: jira
status: ready
execution_type: manual
tags: [feat:credentials, feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#3267]
---
# ELITEA-1530: Jira index_data with invalid credentials returns authentication error instead of misleading success

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Objective: Verify that running index_data on a Jira Toolkit configured with a valid instance URL but invalid credentials (username and API token) returns a clear authentication error — not a misleading success response.

Coverage:
- index_data tool execution with invalid credentials via Toolkit Test Settings
- Index creation and indexing job behavior via the Indexes tab with invalid credentials

## Preconditions

- Logged in to ELITEA
- A valid Jira instance URL is available (e.g. https://your-org.atlassian.net)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Toolkits & Credentials, create a new Jira credential with a valid instance URL but invalid username and API token. Save it. | Credential saved successfully |
| 2 | Create a Jira Toolkit using the invalid credential from step 1. | Toolkit created |
| 3 | Open the toolkit → Toolkit Test Settings → run the index_data tool. | Response contains a clear authentication error: "Failed to instantiate toolkit 'Jira_with_valid_url_invalid_cred': Authentication failed: Invalid username or API key." — NOT {"status": "ok", "message": "no new documents to index"} |
| 4 | Navigate to the Indexes tab → create an index for the toolkit and trigger indexing. | Indexing job fails with: "Failed to instantiate toolkit 'Jira_with_valid_url_invalid_cred': Authentication failed: Invalid username or API key." — NOT {"status": "ok", "message": "no new documents to index"} |

## Expected Final State

Indexing job fails with: "Failed to instantiate toolkit 'Jira_with_valid_url_invalid_cred': Authentication failed: Invalid username or API key." — NOT {"status": "ok", "message": "no new documents to index"}

## Pass/Fail Criteria

Pass:
- index_data returns a clear authentication error message
- Indexing job fails with a visible authentication error

Fail:
- index_data returns {"status": "ok", "message": "no new documents to index"} despite invalid credentials (bug #3267)
- Indexing job reports success with "no new documents to index" despite invalid credentials
