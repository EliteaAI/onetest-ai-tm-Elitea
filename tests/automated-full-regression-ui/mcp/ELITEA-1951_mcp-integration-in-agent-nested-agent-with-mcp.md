---
id: ELITEA-1951
title: "MCP Integration in Agent — Nested Agent with MCP"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1951: MCP Integration in Agent — Nested Agent with MCP

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that a parent agent can invoke a nested sub-agent which has an MCP configured, and that the parent agent's response includes output from the MCP tool used by the sub-agent.

---

## Preconditions

- User is logged in to the Elitea platform.
- A parent agent "ParentAgent" exists or can be created.
- A sub-agent with an MCP configured (e.g., "EliteaMCPAgent") is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Parent Agent | ParentAgent |
| Sub-agent | EliteaMCPAgent |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or use an agent "ParentAgent" | Agent is available |
| 2 | In "Tools" section, click "Agent" tab | Agent tab is active |
| 3 | Attach a sub-agent that has an MCP configured (e.g., "EliteaMCPAgent") | Sub-agent is selected |
| 4 | Verify sub-agent appears in tools list with version selector (e.g., "base" dropdown) | Sub-agent is listed with version selector |
| 5 | Save ParentAgent | Operation completes successfully |
| 6 | Execute ParentAgent — verify it can invoke the sub-agent which uses MCP tools | ParentAgent executes and invokes the sub-agent |
| 7 | Verify response references MCP tool output from nested agent | Response includes output from the MCP tool |

---

## Expected Final State

The parent agent successfully executes and returns a response that includes MCP tool output from the nested sub-agent.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- ParentAgent invokes the sub-agent and returns MCP tool output in the response.

**Fail:**
- Any step produces an error or unexpected result.
- Sub-agent is not invoked or MCP tool output is absent from the response.
