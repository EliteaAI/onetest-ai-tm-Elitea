---
id: ELITEA-0084
title: "Misconfigured MCP (\"Log In\" Required) Is Excluded from Autosuggest"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 5009, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0084: Misconfigured MCP ("Log In" Required) Is Excluded from Autosuggest

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an MCP requiring login/authorization is excluded from the autosuggest dropdown.

**Coverage:** MCP with "Log in" state excluded; properly connected MCPs still shown

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Agent has: one connected MCP AND one MCP showing "Log in" button

## Test Data

Connected MCP name; unauthenticated MCP name

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent in edit mode. Confirm the Toolkits section shows an MCP requiring "Log in". | Both MCPs visible; one shows "Log in". |
| 2 | Expand Instructions, type `/`. | Autosuggest dropdown appears. |
| 3 | Check if the unauthenticated MCP is listed. | It is NOT in the dropdown; the authenticated MCP IS. |

## Expected Final State

It is NOT in the dropdown; the authenticated MCP IS.

## Pass/Fail Criteria

PASS: Unauthenticated MCP absent; authenticated MCP present
FAIL: Unauthenticated MCP appears in the dropdown
