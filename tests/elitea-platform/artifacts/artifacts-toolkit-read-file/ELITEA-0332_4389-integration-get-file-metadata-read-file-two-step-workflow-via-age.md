---
id: ELITEA-0332
title: "[#4389] Integration — get_file_metadata + read_file Two-Step Workflow via Agent Chat and Pipeline Toolkit Node"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, integration, issue:4389, read_file, pipeline, r-2.0.3, agent, excel]
requirements: [4389]
---
# ELITEA-0332: [#4389] Integration — get_file_metadata + read_file Two-Step Workflow via Agent Chat and Pipeline Toolkit Node

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** End-to-end verification of the two-step Excel workflow in real integration contexts: (1) LLM-driven Agent Chat where the agent autonomously calls `get_file_metadata` to discover sheets and then `read_file` with a row range; (2) Pipeline Toolkit Node calling `read_file` with `start_row`/`end_row` on an Excel file.

## Preconditions

User is logged in to ELITEA.
An Agent is configured with the Artifacts Toolkit added as a tool.
`multi_sheet.xlsx` is uploaded to an accessible artifact bucket.
A Pipeline with a Toolkit Node referencing the Artifacts Toolkit exists (or can be created).
The pipeline Toolkit Node can call `read_file` with parameters.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent Chat for the agent configured with Artifacts Toolkit. Send the message: "What sheets are in the file multi_sheet.xlsx in bucket [bucket_name]?" | The agent autonomously calls `get_file_metadata` on the file and returns a list of sheet names to the user in the chat response. No manual parameter input required from the user. |
| 2 | In the same Agent Chat, follow up: "Read rows 5 to 15 from the 'Data' sheet of multi_sheet.xlsx." | The agent calls `read_file` with `sheet_name='Data'`, `start_row=5`, `end_row=15`. Rows 5–15 of the 'Data' sheet are returned in the chat response. No rows outside that range are included. |
| 3 | Open the Pipeline editor. Configure a Toolkit Node to call `read_file` on `multi_sheet.xlsx` with: - `sheet_name`: "Data" - `start_row`: 1 - `end_row`: 10 Save the pipeline and run it. | Pipeline run completes successfully. The Toolkit Node step in run history shows the `read_file` call was made with the specified parameters. Rows 1–10 of the 'Data' sheet are visible in the pipeline run output. |

## Expected Final State

Pipeline run completes successfully. The Toolkit Node step in run history shows the `read_file` call was made with the specified parameters. Rows 1–10 of the 'Data' sheet are visible in the pipeline run output.

## Pass/Fail Criteria

PASS: Agent discovers sheets autonomously; correct rows returned in chat; pipeline Toolkit Node completes with correct row output.
FAIL: Agent fails to call the tools; wrong rows or sheets returned; pipeline node errors; LLM ignores new parameters.
