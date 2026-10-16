---
id: ELITEA-3957
title: "Headless/API run with auto_skip enabled does not hang when Skill or Project Context creation would trigger clarification"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, headless, auto-skip, ask-user]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3957: Headless/API run with auto_skip enabled does not hang when Skill or Project Context creation would trigger clarification

## Preconditions

- A headless/API-driven conversation is configured with `auto_skip` enabled
- Skills Builder, Project Context Builder, and Ask User are all enabled

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Submit an ambiguous Skill creation request via the API (e.g. missing description/target audience) | The run completes without hanging; it produces a defined outcome such as default assumptions applied or a clear non-blocking response, per existing `auto_skip` behavior |
| 2 | Repeat with an ambiguous Project Context creation/update request via the API | The run completes without hanging, with the same `auto_skip`-consistent defined outcome |

## Expected Final State

Headless/API runs using `auto_skip` never hang indefinitely on a clarification pause triggered by the new builders.

## Pass/Fail Criteria

**Pass:**
- Both API runs reach a terminal state within the expected time
- Outcome matches documented auto_skip behavior (defaults applied or explicit non-blocking response)

**Fail:**
- Either run hangs indefinitely waiting on a clarification pause
