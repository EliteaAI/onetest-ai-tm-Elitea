---
id: ELITEA-0035
title: "[Agent] Multiple Toolkits — Parallel `list_collection` Execution Completes Without Error — GPT + Anthropic [Parametrized]"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:collections, feat:toolkits, eng:backend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4959]
---
# ELITEA-0035: [Agent] Multiple Toolkits — Parallel `list_collection` Execution Completes Without Error — GPT + Anthropic [Parametrized]

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when an agent with multiple different toolkit types (GitHub, Jira, Confluence, Artifact) executes `list_collection` on all of them simultaneously in parallel, no `langchain_pg_collection` table conflict error occurs and each toolkit returns its own correct collections.

**Coverage:**
- Parallel invocation of `list_collection` across 3+ different toolkit types
- No `langchain_pg_collection` table conflict error on first and subsequent parallel calls
- Each toolkit returns its own distinct collections — no data missing or cross-contaminated
- Verified with both GPT and Anthropic models

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- An agent has 3–4 toolkits configured, each with the `list_collection` tool (e.g., GitHub, Jira, Confluence, Artifact)
- Note the expected collections per toolkit before running
- Run twice — once per model variant: Run A: GPT-5.2 or GPT-5.4 / Run B: Claude Sonnet 4.5 or 4.6

## Test Data

- Toolkits: GitHub, Jira, Confluence, Artifact (each with list_collection and at least 1 known collection)
- Run A: GPT-5.2 or GPT-5.4
- Run B: Claude Sonnet 4.5 or 4.6 (Anthropic)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent and set the LLM model for the current run (A: GPT or B: Anthropic). | Model configured on the agent. |
| 2 | Send the prompt: "Call the list_collection tool from ALL available toolkits at the same time, in parallel. Do not call them one by one — invoke all simultaneously and return the results from each toolkit separately." | Agent invokes list_collection across all toolkits in parallel simultaneously. |
| 3 | Observe the response and any error messages. | No langchain_pg_collection table conflict error appears. All toolkits return their collections. Each toolkit's results match its known expected collections — no cross-contamination or missing data. |
| 4 | Send the same prompt again without reloading the page. | Second parallel execution also completes without error. Results are consistent with the first call. |
| 5 | Repeat steps 1–4 for the other model variant. | Both GPT and Anthropic variants produce correct results with no errors. |

## Expected Final State

Both GPT and Anthropic variants produce correct results with no errors.

## Pass/Fail Criteria

**Pass:**
- No conflict error in any run
- All toolkits return their own correct collections
- Both LLM model variants behave correctly

**Fail:**
- langchain_pg_collection table conflict error appears with either model
- Any toolkit returns empty or another toolkit's collections
- Results inconsistent between first and second parallel call
