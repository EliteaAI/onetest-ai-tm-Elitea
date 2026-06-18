---
id: ELITEA-0901
title: "Agent and LLM Nodes Receive File Name in Input Mapping via Run Details/History"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0901: Agent and LLM Nodes Receive File Name in Input Mapping via Run Details/History

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that the LLM node nad the Agent node receive the attached file reference during pipeline execution, and that this is visible in run history.

**Coverage:**
- File path and name present in at least one step of the run history
- Agent node input contains the file content or file reference passed from the preceding step
- LLM node input contains the attached file reference
- Pipeline run completes without errors at both nodes

## Preconditions

- Logged in — Private project
- Pipeline A: Allow Attachments enabled, contains an Agent node
- Pipeline B: Allow Attachments enabled, contains an LLM node
- Paperclip icon active in the test chat panel for both pipelines

## Test Data

- File: report.pdf
- Prompt: "Analyze the attached report."
- Pipeline A: pipeline with Agent node
- Pipeline B: pipeline with LLM node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Pipeline A (Agent node). Attach report.pdf in the test chat. Type 'Analyze the attached report.' and click Send. | Pipeline run starts. |
| 2 | Wait for the run to complete. Open Run History and click the latest run. | Run details open showing the timeline with execution steps. |
| 3 | Browse through the steps in the timeline and inspect their details. | At least one step contains the file path and filename report.pdf. |
| 4 | Locate the Agent node step in the timeline and inspect its input_attachments variable. | The Agent node input_attachments variable contains the file reference (file path and name of report.pdf). |
| 5 | Confirm the run status. | Run completed successfully — no errors at the Agent node. |
| 6 | Repeat steps 1–5 using Pipeline B (LLM node). Locate the LLM node step in the timeline and inspect its input. | At least one step contains the file path and filename report.pdf. The LLM node input contains the attached file reference. Run completes successfully with no errors at the LLM node. |

## Expected Final State

At least one step contains the file path and filename report.pdf. The LLM node input contains the attached file reference. Run completes successfully with no errors at the LLM node.

## Pass/Fail Criteria

**Pass:**
- At least one run history step contains the file path and filename report.pdf
- Agent node input contains the file reference or content from the preceding step
- LLM node input contains the attached file reference
- Pipeline run completes without errors at both nodes

**Fail:**
- File path/name absent from all run history steps
- Agent node input does not reference the file
- LLM node input does not reference the file
- Pipeline errors at either node when a file is attached
