---
id: ELITEA-1086
title: "Warning displayed when adding toolkit with missing private credentials to Agent"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:agents, issue:4391, feat:chat, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4391]
---
# ELITEA-1086: Warning displayed when adding toolkit with missing private credentials to Agent

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a user attempts to add a toolkit requiring private credentials to an Agent configuration and the user lacks the required credentials, a clear warning message is displayed in the Agent configuration interface.

**Coverage:**
- Warning message displayed in Agent configuration when credentials missing
- Agent configuration does not proceed silently with missing credentials
- User is informed about credential requirements
- Warning is consistent with Chat warning behavior

## Preconditions

- User is authenticated in ELITEA at {{base_url}}
- User has access to Agents page
- A toolkit requiring private credentials exists
- User does NOT have the required private credentials configured
- Browser: Chrome/Edge latest

## Test Data

- Toolkit: GitHub or Jira (requiring private credentials)
- User account without required private credentials
- Agent name: "Test Agent Credentials Warning"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents page and create or edit an agent | Agent configuration page loads |
| 2 | In the Toolkits section, attempt to add a toolkit requiring private credentials | Toolkit selection interface appears |
| 3 | Select a toolkit that requires private credentials (user does not have these credentials) | Warning message is displayed in Agent configuration indicating missing private credentials |
| 4 | Verify the warning message content and positioning | Warning clearly states which credentials are missing and appears in the Agent configuration form |
| 5 | Attempt to save the agent configuration | Save is blocked or warning persists until credentials are configured |

## Expected Final State

Save is blocked or warning persists until credentials are configured

## Pass/Fail Criteria

**Pass:**
- Warning message is displayed in Agent configuration
- Warning clearly states missing private credentials
- User cannot save agent configuration without addressing credentials
- Warning provides actionable guidance

**Fail:**
- No warning is shown in Agent configuration
- Agent saves silently with missing credentials
- User is not informed about missing credentials
- Agent fails at runtime without prior warning
