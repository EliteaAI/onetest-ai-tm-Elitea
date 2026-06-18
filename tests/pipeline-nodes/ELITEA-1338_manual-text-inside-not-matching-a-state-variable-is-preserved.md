---
id: ELITEA-1338
title: "Manual Text Inside {} Not Matching a State Variable Is Preserved"
priority: high
type: functional
module: pipeline-nodes
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2626]
---
# ELITEA-1338: Manual Text Inside {} Not Matching a State Variable Is Preserved

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can type text inside curly brackets that does not match any state variable, and the text is accepted and preserved as typed — not auto-deleted, replaced, or rejected.

**Coverage:**
- Non-matching text after `{` results in empty/no-match dropdown state
- User can complete `{custom_label}` manually
- Value persists in YAML exactly as entered
- Unresolved `{custom_label}` appears literally in pipeline output

## Preconditions

- Logged into {{base_url}}
- Pipeline with state variables `input` and `project_id`
- LLM node Task field set to F-String, pipeline connected end-to-end

## Test Data

Non-variable text: `{custom_label}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open LLM node Task field (F-String). Type `{`. When dropdown appears, continue typing `custom_label`. | Dropdown shows no matching suggestions or an empty/no-results state. No auto-replacement occurs. |
| 2 | Press Escape to dismiss the dropdown (if still visible). Type `}` to complete: `{custom_label}`. Save the node and pipeline. | Field contains `{custom_label}`. Pipeline saves successfully without error. |
| 3 | Switch to YAML view. Locate the LLM node task field value. | YAML value is exactly `{custom_label}` — no modification, no removal. |
| 4 | Run the pipeline via Chat. | Output contains the literal string `{custom_label}` — it is not substituted with any value and no error is thrown for the unrecognized variable. |

## Expected Final State

Output contains the literal string `{custom_label}` — it is not substituted with any value and no error is thrown for the unrecognized variable.

## Pass/Fail Criteria

**Pass:**
- Non-variable text is accepted and preserved in YAML
- Literal `{custom_label}` appears in runtime output without error

**Fail:**
- Text is auto-deleted or blocked
- Pipeline errors out due to unrecognized variable reference
