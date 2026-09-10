---
id: ELITEA-3367
title: "Skill creation from chat with missing information triggers Ask User clarification"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, story:6239, regression, skills-builder, ask-user, clarifying-question]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3367: Skill creation from chat with missing information triggers Ask User clarification

## Objective

Verify that an incomplete Skill creation request triggers the Ask User clarification flow, and submitted answers are used to complete the Skill creation.

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder is enabled in Chat Modules
- Ask User is enabled in Chat Modules

## Test Data

| Field | Value |
|-------|-------|
| Initial request | "Create a skill for onboarding" (no description, audience, or instructions given) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the incomplete Skill creation request: "Create a skill for onboarding" | A clarifying-question card appears with 1 to 4 structured questions covering missing required fields |
| 2 | Verify question card UI | Questions are displayed with appropriate input controls (single-select, multi-select, or free-text as applicable) |
| 3 | Answer all questions and click Submit | The clarification card closes |
| 4 | Verify clarification card does not reappear | The same clarification card is not shown again for this request |
| 5 | Verify Skill is created | A Skill chip/link appears in the chat response |
| 6 | Click the Skill chip and inspect fields | Skill fields reflect the answers submitted in the clarification step |

## Expected Final State

Missing Skill information triggers Ask User exactly once, submitted answers are used to create the Skill correctly.

## Pass/Fail Criteria

**Pass:**
- Clarifying question card appears for missing required fields
- Questions display with appropriate input controls
- Skill created using the submitted answers
- Clarification card is not re-shown after submission
- Skill chip displayed and links to correct Skill

**Fail:**
- Assistant guesses missing fields without asking
- Clarification card does not appear
- Skill fields do not reflect submitted answers
- Clarification card reappears after submission
