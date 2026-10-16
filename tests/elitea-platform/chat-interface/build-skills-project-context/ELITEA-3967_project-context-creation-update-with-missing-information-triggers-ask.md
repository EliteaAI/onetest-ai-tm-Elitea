---
id: ELITEA-3967
title: "Project Context creation/update with missing information triggers Ask User clarification and resumes correctly"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, ask-user]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3967: Project Context creation/update with missing information triggers Ask User clarification and resumes correctly

## Preconditions

- User is logged in to `{{base_url}}`
- Project Context Builder and Ask User are enabled

## Test Data

| Field | Value |
|-------|-------|
| Initial request | "Set up project context for this." (scope unspecified) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the ambiguous Project Context request | A clarifying-question card appears, including a question about intended scope (e.g. current project only / all conversations in the project / a specific Agent or Pipeline) |
| 2 | Select an answer and submit | The clarification card closes and is not shown again for this request |
| 3 | Inspect the created/updated Project Context | The scope and content reflect the submitted answer |

## Expected Final State

Missing Project Context information triggers Ask User exactly once, and the submitted answer determines the resulting scope/content.

## Pass/Fail Criteria

**Pass:**
- Clarifying question about scope (or other missing field) is shown
- Resulting Project Context reflects the submitted answer
- Clarification card is not re-shown

**Fail:**
- Assistant guesses scope/content without asking
- Resulting entity does not reflect the submitted answer
