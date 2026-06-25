---
id: ELITEA-1768
title: "Code Node debug:true — Artifact Saved to code-debug Bucket With Correct Filename and Content"
priority: critical
type: functional
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5203]
---
# ELITEA-1768: Code Node `debug: true` — Artifact Saved to `code-debug` Bucket

**Module:** Pipelines / Code Node · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a pipeline code node has `debug: true`, the fully-assembled Python code is saved to the `code-debug` artifact bucket after execution, with filename `<NodeName>__<YYYYMMDD>_<HHMMSS>.py` and content containing the full state preamble plus user code.

## Preconditions

- A pipeline exists with at least one code node
- `debug: true` is set on the code node in the pipeline YAML
- The `code-debug` artifact bucket may or may not exist (auto-creation is expected)
- User has access to the Artifacts section in the platform

## Test Data

| Field | Value |
|-------|-------|
| Pipeline | Any pipeline with a code node |
| Code node `debug` flag | `true` |
| Code node id/name | e.g., `process_data` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline YAML and set `debug: true` on a code node; save | Pipeline saved successfully |
| 2 | Run the pipeline | Pipeline executes; code node runs |
| 3 | Navigate to **Artifacts → `code-debug` bucket** | `code-debug` bucket exists (auto-created if it didn't exist before) |
| 4 | Verify a new `.py` file is present | File named `<NodeName>__<YYYYMMDD>_<HHMMSS>.py` (e.g., `process_data__20260624_163735.py`) |
| 5 | Download and open the artifact file | File content contains the state preamble (`elitea_state`, `elitea_client`, base64-compressed state) followed by the user code |
| 6 | Verify the user code section is present and correct | The user-written code from the node appears after the preamble comment `# --- user code below ---` |

## Expected Final State

`code-debug` bucket contains a timestamped `.py` artifact for the executed node. File contains full assembled code (preamble + user code).

## Pass/Fail Criteria

**Pass:**
- `code-debug` bucket auto-created if it didn't exist
- Artifact file present with `<NodeName>__<timestamp>.py` naming
- File contains state preamble and user code
- Pipeline completed successfully

**Fail:**
- No artifact saved after execution
- Artifact saved to wrong bucket or wrong filename format
- File content missing preamble or user code
- Pipeline fails due to artifact save operation
