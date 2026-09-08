---
id: ELITEA-3312
title: "Pipeline Builder continues to receive context as before with no regression"
priority: high
type: regression
module: pipelines
status: ready
execution_type: manual
tags: [feat:context-management, feat:toolkits, story:6306, r-2.0.6, pipeline-builder, regression]
requirements: [EliteaAI/elitea_issues#6306]
---

# ELITEA-3312: Pipeline Builder continues to receive context as before with no regression

## Preconditions

- User is logged in to `{{base_url}}`
- Agent & Pipeline Builder module is enabled
- User has successfully created pipelines via chat before (baseline behavior known)

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enable Agent & Pipeline Builder in Chat Modules | Module is enabled |
| 2 | Send: "Create a pipeline called 'Text Summarizer' that takes text input and produces a summary using an LLM" | Assistant proceeds with pipeline creation |
| 3 | If clarifying questions are asked (Ask User flow), answer them | Flow continues as expected |
| 4 | Verify the pipeline is created successfully | Pipeline chip/link appears in chat response |
| 5 | Click the pipeline chip to open the pipeline | Pipeline opens correctly in editor mode |
| 6 | Navigate to Pipelines list and verify the pipeline appears in current project | Pipeline is listed in the correct project |
| 7 | Test the created pipeline by executing it | Pipeline runs successfully |

## Expected Final State

Pipeline Builder behavior is completely unchanged by the runtime_context enhancement to Project Context Builder and Skill Builder. The existing context injection for Pipeline Builder continues to work.

## Pass/Fail Criteria

**Pass:**
- Pipeline creation completes successfully as before
- Pipeline appears in the correct project
- All existing Pipeline Builder features work correctly
- No changes to Pipeline Builder user experience

**Fail:**
- Pipeline creation behavior changed
- Pipeline appears in wrong project
- New errors or regressions in Pipeline Builder
- Context injection broken for Pipeline Builder
