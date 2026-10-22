---
id: ELITEA-3811
title: "Agent with multiple Jira toolkit tools using normalized URL"
priority: high
type: integration
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, feat:agents, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Jira toolkit is configured with base_url containing trailing slash (e.g., `https://jiraeu.epam.com/`)
- Check Connection for Jira toolkit passed successfully
- User has access to Agents section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Jira base_url | `https://jiraeu.epam.com/` (with trailing slash) |
| Jira project key | Valid project key |
| Agent name | `Multi-Tool Jira Agent - URL Normalization Test` |
| Jira tools to enable | Search Issues, Get Issue, Create Issue, Update Issue, Add Comment |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents section | Agents page loads successfully |
| 2 | Create a new agent | Agent creation page opens |
| 3 | Add Jira toolkit to the agent | Jira toolkit added |
| 4 | Enable multiple Jira tools: Search Issues, Get Issue, Create Issue, Update Issue, Add Comment | All 5 tools enabled and visible |
| 5 | Save the agent configuration | Agent saved successfully |
| 6 | Open the agent in Chat | Agent ready for interaction |
| 7 | Send message: "Search for open issues in project [KEY]" | Agent invokes Search Issues tool successfully |
| 8 | Verify search results are displayed | Valid issue list displayed |
| 9 | Send message: "Get details for issue [KEY-123]" | Agent invokes Get Issue tool successfully |
| 10 | Verify issue details are displayed | Full issue details displayed |
| 11 | Send message: "Create a new issue with summary 'Test issue'" | Agent invokes Create Issue tool successfully |
| 12 | Verify issue creation success | New issue created, issue key returned |
| 13 | Send message: "Update issue [KEY-123] description to 'Updated via agent'" | Agent invokes Update Issue tool successfully |
| 14 | Verify update success | Issue updated confirmation |
| 15 | Send message: "Add comment to issue [KEY-123]: 'Test comment'" | Agent invokes Add Comment tool successfully |
| 16 | Verify comment added | Comment added confirmation |
| 17 | Execute all 5 operations in a single agent session | All tools execute successfully without URL errors |

## Expected Final State

- Agent successfully executes all 5 Jira toolkit tools in same session
- All Jira API calls use normalized base_url correctly
- No URL-related errors across multiple tool invocations
- Agent maintains consistent toolkit connection throughout session

## Pass/Fail Criteria

**Pass:**
- All 5 Jira tools execute successfully in agent workflow
- Multiple sequential tool calls work without errors
- Each tool invocation returns valid data
- No URL-related errors in any tool call
- Jira client maintains consistent connection across tools
- All API endpoints constructed correctly (no double slashes)

**Fail:**
- Any Jira tool fails with URL-related errors
- Sequential tool calls fail after first success
- Jira client connection breaks between tool calls
- Malformed URLs generated in any tool invocation
- Agent session interrupted by toolkit errors
