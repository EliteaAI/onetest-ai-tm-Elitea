---
id: ELITEA-0129
title: "Swarm Mode - Child Agent Toolkit Invocation"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: []
requirements: []
---
# ELITEA-0129: Swarm Mode - Child Agent Toolkit Invocation

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that child agents in swarm mode can successfully invoke their configured toolkits (Jira, GitHub, Bitbucket, etc.).

## Preconditions

User logged into Elitea stage.elitea.ai\nChild agent exists with a configured toolkit (e.g., Jira, GitHub)\nToolkit credentials are valid and tested independently\nParent swarm agent exists with child agent associated

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a child agent with a Jira toolkit configured (valid credentials, tested independently) | Child agent created with Jira toolkit; toolkit works when tested on the child agent directly |
| 2 | Verify the child agent can invoke the Jira toolkit independently (outside swarm mode) by sending a chat request like 'List Jira issues in project X' | Child agent successfully invokes Jira toolkit and returns results (baseline test) |
| 3 | Create a parent swarm agent with Swarm Mode enabled and add the child agent | Parent swarm agent configured with child agent |
| 4 | Open the parent swarm agent chat and send a request requiring Jira toolkit invocation (e.g., 'Check the status of Jira ticket ABC-123') | Parent agent delegates to child agent; child agent invokes Jira toolkit; results returned in chat |
| 5 | Verify the chat output shows toolkit execution results (not just the delegation to child agent) | Chat output includes actual Jira data (ticket status, details, etc.) |
| 6 | Repeat steps 1-5 with a GitHub toolkit configured on a different child agent | GitHub toolkit invocation also works correctly through swarm mode |
| 7 | Test with a mixed request requiring both Jira and GitHub child agents | Both child agents invoke their respective toolkits successfully |

## Expected Final State

Both child agents invoke their respective toolkits successfully

## Pass/Fail Criteria

Child agent toolkit invocation succeeds in swarm mode\nToolkit execution results visible in chat (not just delegation)\nResults match independent child agent toolkit invocation\nNo errors related to toolkit access or permissions in swarm context
