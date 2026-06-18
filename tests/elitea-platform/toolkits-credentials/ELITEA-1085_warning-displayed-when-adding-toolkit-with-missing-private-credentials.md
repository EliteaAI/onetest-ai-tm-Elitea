---
id: ELITEA-1085
title: "Warning displayed when adding toolkit with missing private credentials to Chat"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:agents, issue:4391, feat:chat, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4391]
---
# ELITEA-1085: Warning displayed when adding toolkit with missing private credentials to Chat

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a user attempts to add a toolkit requiring private credentials to a Chat conversation and the user lacks the required credentials, a clear warning message is displayed before the toolkit is added.

**Coverage:**
- Warning message displayed when private credentials are missing
- Toolkit addition blocked or warned in Chat context
- User is informed about missing credential requirement
- No silent toolkit addition with missing credentials

## Preconditions

- User is authenticated in ELITEA at {{base_url}}
- User has access to Chat interface
- A toolkit requiring private credentials exists (e.g., Jira, GitHub)
- User does NOT have the required private credentials configured
- Browser: Chrome/Edge latest

## Test Data

- Toolkit: Jira (or any toolkit requiring private credentials)
- User account without required private credentials
- Chat conversation URL

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat interface in ELITEA | Chat interface loads successfully |
| 2 | Attempt to add a toolkit (e.g., Jira) that requires private credentials to the chat | Toolkit addition interface appears |
| 3 | Select a toolkit that requires private credentials (user does not have these credentials) | Warning message is displayed indicating missing private credentials |
| 4 | Verify the warning message content | Warning clearly states which credentials are missing and provides guidance to create them |

## Expected Final State

Warning clearly states which credentials are missing and provides guidance to create them

## Pass/Fail Criteria

**Pass:**
- Warning message is displayed when adding toolkit to Chat
- Warning clearly states missing private credentials
- User cannot silently add toolkit without credentials
- Warning provides guidance on how to create credentials

**Fail:**
- No warning is shown
- Toolkit is added silently without credentials
- User is not informed about missing credentials
- Chat fails without clear error message
