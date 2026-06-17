---
id: ELITEA-0359
title: "read_file on file >200k chars via Pipeline Code Node returns full content — no size limit"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: ready
execution_type: manual
tags: [feat:artifacts, issue:4011, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4011]
---
# ELITEA-0359: read_file on file >200k chars via Pipeline Code Node returns full content — no size limit

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Verify that calling read_file via SDK inside a Pipeline Code Node on a file exceeding 200k characters returns the full content with no size-limit constraint.

**Coverage:**
- Pipeline Code Node calls SDK directly — `skip_size_check` not sent → function default `True`
- File >200k returned fully to the code node
- Code node output or state contains actual file content, not error string

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- A Pipeline with a Code Node that uses the Artifact SDK to call read_file
- Test file `xlarge_file.txt` (~300k chars) pre-uploaded to the bucket

## Test Data

- File: `xlarge_file.txt` (~300,000 chars)
- Code Node snippet example:
  ```python
  content = artifact.read_file(filename="xlarge_file.txt")
  return {"file_content": content}
  ```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipeline with the Code Node configured to call read_file on `xlarge_file.txt`. | Pipeline editor opens, Code Node visible. |
| 2 | Run the pipeline. | Pipeline executes. Code Node runs. |
| 3 | Inspect the Code Node output in Run Details. | Output contains full file content (~300k chars). No size-limit error string in the output state. |

## Expected Final State

Output contains full file content (~300k chars). No size-limit error string in the output state.

## Pass/Fail Criteria

**Pass:**
- Full file content present in Code Node output
- No size-limit error string

**Fail:**
- Size-limit error string in Code Node output
- Code Node fails or throws exception related to content size
