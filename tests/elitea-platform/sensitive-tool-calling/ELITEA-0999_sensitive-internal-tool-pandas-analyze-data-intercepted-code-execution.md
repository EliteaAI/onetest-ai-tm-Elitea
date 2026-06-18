---
id: ELITEA-0999
title: "Sensitive Internal Tool (pandas_analyze_data) Intercepted — Code Execution Guardrail"
priority: high
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-0999: Sensitive Internal Tool (pandas_analyze_data) Intercepted — Code Execution Guardrail

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that the authorization guardrail intercepts internal data analysis tools (pandas_analyze_data) configured as sensitive, pausing code execution until the user explicitly authorizes or blocks it.

## Preconditions

- The pandas > pandas_analyze_data tool is configured as sensitive in Admin UI → Configuration → Guardrails
- An agent with the Pandas toolkit (bucket configured) is available
- A data file (e.g., sales_data.csv) exists in the configured artifact bucket

## Test Data

- Sensitive tool: pandas.pandas_analyze_data
- File in bucket: sales_data.csv
- Agent prompt: 'Analyze sales_data.csv and calculate total revenue by region'
- Parameters expected in dialog: query: 'calculate total revenue by region', filename: 'sales_data.csv'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. Enable data_analysis > pandas_analyze_data as a sensitive tool. Save and restart services. | Configuration saved successfully. |
| 2 | Open the agent with the Pandas toolkit configured. Send the analysis prompt: 'Analyze sales_data.csv and calculate total revenue by region'. | Agent begins processing. |
| 3 | Observe the chat area before any data analysis code executes. | Authorization dialog appears with title '⚠️ Sensitive Action Authorization Required'. The Pyodide/pandas code has NOT executed yet. |
| 4 | Verify the dialog shows action name data_analysis.pandas_analyze_data (or equivalent toolkit.tool label). | Action name is displayed prominently in the dialog. |
| 5 | Verify the Parameters section shows query and filename values. | query: 'calculate total revenue by region' and filename: 'sales_data.csv' are displayed. |
| 6 | Click [Authorize]. | Dialog closes. The pandas_analyze_data tool executes. Python/pandas code runs in the sandbox. Agent returns the analysis result (e.g., revenue breakdown). |
| 7 | Trigger the same prompt again. When the dialog appears, click [Block]. | Dialog closes. No Python code is executed. Agent acknowledges the block. No data analysis result is returned. |
| 8 | Verify no side-effect files (e.g., chart PNGs) were created in the artifact bucket after Block. | Artifact bucket contains no new chart or output files from the blocked run. |

## Expected Final State

Artifact bucket contains no new chart or output files from the blocked run.

## Pass/Fail Criteria

Pass:
- Authorization dialog appears before pandas/Pyodide code executes
- Parameters (query, filename) visible in the dialog
- Authorize: code executes and analysis result is returned by the agent
- Block: no code executes, no chart/output files created in the bucket
- Agent responds correctly in both Authorize and Block cases

Fail:
- Data analysis code executes without showing any dialog
- Dialog appears after the code has already run (side effects already occurred)
- Block does not prevent code execution (charts are still saved to bucket)
