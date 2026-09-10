---
id: ELITEA-3369
title: "Project Context creation with missing information triggers Ask User clarification"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, story:6239, regression, project-context-builder, ask-user, clarifying-question]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3369: Project Context creation with missing information triggers Ask User clarification

## Objective

Verify that an ambiguous Project Context creation request triggers the Ask User clarification flow, and submitted answers are used to complete the creation correctly.

## Preconditions

- User is logged in to `{{base_url}}`
- Project Context Builder is enabled in Chat Modules
- Ask User is enabled in Chat Modules

## Test Data

| Field | Value |
|-------|-------|
| Initial request | "Set up project context for this." (scope unspecified) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the ambiguous Project Context request: "Set up project context for this." | A clarifying-question card appears, including a question about intended scope |
| 2 | Verify question card includes scope options | Question asks about scope (e.g., current project only / all conversations / specific Agent or Pipeline) |
| 3 | Select an answer for scope and submit | The clarification card closes |
| 4 | Verify clarification card does not reappear | The same clarification card is not shown again for this request |
| 5 | Verify Project Context is created | A Project Context chip/link appears in the chat response |
| 6 | Click the chip and inspect the created Project Context | Scope and content reflect the submitted answer |

## Expected Final State

Missing Project Context information triggers Ask User exactly once, submitted answer determines the resulting scope/content.

## Pass/Fail Criteria

**Pass:**
- Clarifying question about scope (or other missing field) is shown
- Question card closes after submission
- Resulting Project Context reflects the submitted answer
- Clarification card is not re-shown

**Fail:**
- Assistant guesses scope/content without asking
- Clarification card does not appear
- Resulting entity does not reflect the submitted answer
- Clarification card reappears after submission
