---
id: ELITEA-0946
title: "Pipeline LLM Node Does Not Crash When Project Context Is Enabled"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, story:3395, pipeline, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395, EliteaAI/elitea_issues#5316]
---
# ELITEA-0946: Pipeline LLM Node Does Not Crash When Project Context Is Enabled

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that enabling Project Context does not cause pipeline LLM nodes to crash with a YAML parsing error, and that context is not injected into pipelines.

**Coverage:**
- Pipeline executes without YAML parsing crash when context is enabled
- Context content is not injected into pipeline execution
- Pipeline works with toggle both ON and OFF

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Project Context content: `Return all in lowercase always`
- Pipeline with at least one LLM node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Project Context. Set content to: 'Return all in lowercase always'. Toggle = ON. Save. | Content and toggle saved. |
| 2 | Run a pipeline containing an LLM node. | Pipeline executes WITHOUT crash. No YAML parsing error appears in logs or UI. |
| 3 | Ask the pipeline: 'What special instructions do you have about text formatting?' | Pipeline does NOT apply the lowercase rule. Project Context is not injected into the pipeline. |
| 4 | Disable Enable Project Context toggle. Run the pipeline again. | Pipeline executes cleanly with toggle OFF as well. |

## Expected Final State

Pipeline executes cleanly with toggle OFF as well.

## Pass/Fail Criteria

**Pass:**
- Pipeline runs without YAML parsing error
- Pipeline does not apply Project Context content
- No crash with toggle ON or OFF

**Fail:**
- Pipeline crashes with YAML ComposerError or similar
- Pipeline applies the lowercase rule from context
