---
id: ELITEA-0001
title: "[Chat] Multiple Toolkits — Parallel list_collection Execution Completes Without Error — GPT + Anthropic [Parametrized]"
priority: high
type: regression
module: agents
status: ready
execution_type: manual
tags: [feat:collections, feat:toolkits, eng:backend]
requirements: [EliteaAI/elitea_issues#4959]
---

# ELITEA-0001: [Chat] Multiple Toolkits — Parallel list_collection Execution Completes Without Error — GPT + Anthropic [Parametrized]

**Module:** Agents · **Priority:** High · **Type:** Regression

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)
- Chat configured with 3–4 toolkits each having `list_collection` (e.g., GitHub, Jira, Confluence, Artifact)
- Note the expected collections per toolkit before running
- Run twice — once per model variant:
  - Run A: GPT-5.2 or GPT-5.4
  - Run B: Claude Sonnet 4.5 or 4.6

## Test Data

| Field       | Value                                                                                 |
|-------------|---------------------------------------------------------------------------------------|
| Toolkits    | GitHub, Jira, Confluence, Artifact (each with `list_collection` and ≥1 known collection) |
| Run A model | GPT-5.2 or GPT-5.4                                                                    |
| Run B model | Claude Sonnet 4.5 or 4.6 (Anthropic)                                                 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat session and set the LLM model for the current run (A: GPT or B: Anthropic). | Chat loads with model configured. |
| 2 | Send the prompt: "Call the `list_collection` tool from ALL available toolkits at the same time, in parallel. Do not call them one by one — invoke all simultaneously and return the results from each toolkit separately." | Chat invokes `list_collection` across all toolkits in parallel simultaneously. |
| 3 | Observe the response and any error messages. | No `langchain_pg_collection` table conflict error appears. All toolkits return their collections. Each toolkit's results match its known expected collections — no cross-contamination or missing data. |
| 4 | Send the same prompt again without reloading the page. | Second parallel execution also completes without error. Results consistent with the first call. |
| 5 | Repeat steps 1–4 for the other model variant. | Both GPT and Anthropic variants produce correct results with no errors. |

## Expected Final State

Both GPT and Anthropic model variants complete parallel `list_collection` invocations across all configured toolkits without errors. Each toolkit returns its own correct, distinct collections with no cross-contamination or missing data. No `langchain_pg_collection` table conflict error occurs on first or subsequent calls.

## Pass/Fail Criteria

**Pass:**
- No conflict error in Chat context with either model
- All toolkits return their own correct collections
- Both model variants behave correctly

**Fail:**
- `langchain_pg_collection` table conflict error in Chat context
- Any toolkit returns empty or cross-contaminated collections
- Results differ between first and second parallel call
