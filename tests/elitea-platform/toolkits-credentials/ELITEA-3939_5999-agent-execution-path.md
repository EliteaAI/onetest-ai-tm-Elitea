---
id: ELITEA-3939
title: "[EliteaAI/elitea_issues#5999] Agent/AI Execution Path (Post-Connection)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:jira, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-3939: Agent/AI Execution Path (Post-Connection)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify Jira toolkit works correctly when called from agent/AI conversation (not just manual UI testing).

## Preconditions

- Successful connection test completed (any scenario from ELITEA-2616 or 2618)
- Toolkit configuration saved
- Agent/Chat interface available
- User can compose agent instructions

## Test Data

| Action | Description |
|--------|-------------|
| Search | "Find all open issues in PROJECT" |
| Read | "Get details of issue KEY-123" |
| Write | "Add comment to KEY-123: 'Test comment'" |
| Update | "Change status of KEY-123 to Done" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Chat/Agent, instruct agent: "Search for recent issues in my Jira project". | Agent processes instruction. |
| 2 | Agent calls Jira toolkit search tool. | Search succeeds; issues returned to agent. |
| 3 | Agent includes results in response to user. | Agent can see and reference issue data. |
| 4 | Instruct agent: "Read issue KEY-123 and summarize it". | Agent calls read tool; receives issue details. |
| 5 | Agent summarizes issue in plain English. | Summary is accurate based on Jira data. |
| 6 | Instruct agent: "Add a comment to KEY-123". | Agent calls write tool with comment. |
| 7 | Comment appears in Jira. | Comment visible in Jira UI immediately. |
| 8 | Instruct agent: "Update KEY-123 status". | Agent calls update tool. |
| 9 | Field updated in Jira. | Update reflected in Jira. |
| 10 | Agent does not require manual follow-up or corrections. | Toolkit usage is transparent to agent flow. |

## Expected Final State

- Agent can call Jira tools without special configuration
- All operations (search, read, write, update) work via agent
- Agent receives correct data and can reason about it
- No manual intervention needed after connection test
- Toolkit usage is seamless in agent conversation flow

## Pass/Fail Criteria

**Pass:** All agent operations succeed, no manual fixes, toolkit integration transparent.  
**Fail:** Agent tools fail, manual config needed, agent cannot reason about data, or operations incomplete.

## Notes

- This validates the end-to-end user workflow
- Most important: agent should work WITHOUT manual UI testing first
- Tests that saved configuration is correctly loaded and used
- Critical for production readiness
