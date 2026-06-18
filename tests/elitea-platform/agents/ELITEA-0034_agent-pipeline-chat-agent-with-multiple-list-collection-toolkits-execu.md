---
id: ELITEA-0034
title: "[Agent / Pipeline / Chat] Agent with Multiple `list_collection` Toolkits Executed as Sub-Agent — Parallel Execution Works Correctly [Parametrized]"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:collections, feat:toolkits, eng:backend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4959]
---
# ELITEA-0034: [Agent / Pipeline / Chat] Agent with Multiple `list_collection` Toolkits Executed as Sub-Agent — Parallel Execution Works Correctly [Parametrized]

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an agent configured with multiple `list_collection` toolkits is invoked as a sub-agent from a parent Agent, a Pipeline Agent node, or Chat, parallel `list_collection` execution inside the sub-agent still completes without conflict errors and returns correct collections from each toolkit.

**Coverage:**
- Sub-agent parallel list_collection called from a parent Agent (via Agent toolkit)
- Sub-agent parallel list_collection called from a Pipeline Agent node
- Sub-agent parallel list_collection called from Chat as a participant
- Each toolkit returns its own correct collections in all three calling contexts

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- A sub-agent exists with 3+ toolkits (GitHub, Jira, Confluence, Artifact) each with `list_collection`; its system prompt instructs it to call list_collection on all toolkits in parallel
- Run three variants: A — called from a parent Agent / B — called via a Pipeline Agent node / C — called as a participant from Chat

## Test Data

- Sub-agent toolkits: GitHub, Jira, Confluence, Artifact (each with list_collection)
- Run A: Parent Agent calls sub-agent as a toolkit
- Run B: Pipeline with Agent node pointing to the sub-agent
- Run C: Chat with sub-agent as participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set up the calling context for the current run: Run A — open parent agent that calls the sub-agent as a toolkit. Run B — open a pipeline with an Agent node pointing to the sub-agent. Run C — open Chat with the sub-agent as a participant. | Correct calling context is open and ready. |
| 2 | Send a prompt that triggers the sub-agent: "Ask the sub-agent to call list_collection on ALL its toolkits simultaneously in parallel and return the results from each separately." | Parent delegates to the sub-agent. Sub-agent invokes list_collection on all toolkits in parallel simultaneously. |
| 3 | Observe the full execution response. | No langchain_pg_collection conflict error. Sub-agent returns collections from all toolkits. Each toolkit's results match its known expected collections — no cross-contamination or missing data. |
| 4 | Repeat steps 1–3 for each remaining variant (A / B / C). | All three execution contexts (Agent / Pipeline / Chat) complete without conflict errors and return correct collections. |

## Expected Final State

All three execution contexts (Agent / Pipeline / Chat) complete without conflict errors and return correct collections.

## Pass/Fail Criteria

**Pass:**
- Parallel list_collection inside sub-agent works correctly across all three calling contexts
- No conflict error in any variant
- Each toolkit returns its own correct collections

**Fail:**
- Conflict error surfaces in any of the three contexts
- Collections missing or cross-contaminated when sub-agent executes in parallel
