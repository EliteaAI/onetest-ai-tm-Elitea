---
id: ELITEA-1695
title: "Case-Insensitive Blocked Tool Matching"
priority: high
type: functional
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1695: Case-Insensitive Blocked Tool Matching

**Module:** Admin Portal / Guardrails · **Priority:** High · **Type:** Functional

**Objective:** Verify that blocked tool rules within a specific toolkit are applied correctly regardless of the casing or naming format used in tool invocations.

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- An agent with access to a toolkit containing tools to be blocked (e.g., `github` toolkit with `create_pull_request` tool)

## Test Data

| Toolkit | Configured Blocked Tool | Tool Invocation Variants to Test |
|---------|------------------------|----------------------------------|
| `github` | `create_pull_request` | `Create_Pull_Request`, `CREATE_PULL_REQUEST`, `createPullRequest`, `Create_pull_request` |
| `jira` | `delete_issue` | `Delete_Issue`, `DELETE_ISSUE`, `deleteIssue` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | In "Blocked Tools" section, select `github` toolkit and add `create_pull_request` to blocked tools. | Tool is added to blocked list under github toolkit. |
| 3 | Click "Save Configuration". | Configuration saved successfully. |
| 4 | Open an agent chat with `github` toolkit enabled. | Agent chat opens. |
| 5 | Send a prompt: "Create a pull request for my changes". | The `create_pull_request` tool is blocked. Agent acknowledges it cannot perform this action. |
| 6 | (If MCP integration) Test with MCP server that exposes `Create_Pull_Request` (PascalCase). | Tool is blocked despite different casing. |
| 7 | Test with tool name variant `CREATE_PULL_REQUEST`. | Tool is blocked. |
| 8 | Verify other github tools (e.g., `list_repos`) still work. | Non-blocked tools execute normally. |

## Expected Final State

The specific blocked tool is blocked regardless of casing variations, while other tools in the same toolkit remain functional.

## Pass/Fail Criteria

**Pass:**
- Blocked tool rule applies to all casing variants of the tool name
- `create_pull_request`, `Create_Pull_Request`, `CREATE_PULL_REQUEST` all blocked
- Other tools in the same toolkit are not affected
- Agent correctly acknowledges when a tool is blocked

**Fail:**
- Tool executes when invoked with different casing
- Blocking one tool inadvertently blocks other tools
- Inconsistent behavior between different naming formats
