---
id: ELITEA-3970
title: "Single-question clarification flow shows Submit only, without progress indicator or Back/Next controls"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, ask-user, clarifying-question-ui]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3970: Single-question clarification flow shows Submit only, without progress indicator or Back/Next controls

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder and Ask User are enabled

## Test Data

| Field | Value |
|-------|-------|
| Clarification flow | A request ambiguous in exactly one required field |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a clarification flow that resolves to exactly one question | Only the question and a "Submit" control are shown; no progress indicator, Back, or Next controls are present |
| 2 | Answer the question and click Submit | The flow completes and the original Skill/Project Context request resumes using the submitted answer |

## Expected Final State

A single-question clarification flow shows only a Submit control and resumes the original request correctly.

## Pass/Fail Criteria

**Pass:**
- No progress indicator, Back, or Next shown for a single-question flow
- Submit completes the flow using the submitted answer

**Fail:**
- Progress indicator, Back, or Next erroneously appear for a single question
- Submit fails to resume the original request
