---
id: ELITEA-2792
title: "Optional clarifying question does not block progressing to the next question or submitting"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, ask-user, clarifying-question-ui]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2792: Optional clarifying question does not block progressing to the next question or submitting

## Preconditions

- User is logged in to `{{base_url}}`
- Project Context Builder and Ask User are enabled

## Test Data

| Field | Value |
|-------|-------|
| Clarification flow | Multi-question flow where at least one question is marked optional |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a multi-question clarification flow containing an optional question | The optional question is visually indicated as optional |
| 2 | Leave the optional question unanswered and click Next (or Submit if it is the final question) | The control remains enabled and the flow proceeds/completes without requiring an answer |

## Expected Final State

An unanswered optional clarifying question never blocks progressing through or completing the clarification flow.

## Pass/Fail Criteria

**Pass:**
- Next/Submit remains enabled with the optional question unanswered
- Flow proceeds/completes successfully

**Fail:**
- Next/Submit is blocked by an unanswered optional question
