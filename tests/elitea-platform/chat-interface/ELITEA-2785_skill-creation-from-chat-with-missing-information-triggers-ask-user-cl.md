---
id: ELITEA-2785
title: "Skill creation from chat with missing information triggers Ask User clarification and resumes correctly with submitted answers"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, skills-builder, ask-user]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2785: Skill creation from chat with missing information triggers Ask User clarification and resumes correctly with submitted answers

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder and Ask User are enabled

## Test Data

| Field | Value |
|-------|-------|
| Initial request | "Create a skill for onboarding" (no description, audience, or instructions given) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the incomplete Skill creation request | A clarifying-question card appears with 1 to 4 structured questions covering the missing required fields |
| 2 | Answer all questions and submit | The clarification card closes; the same card is not shown again for this request |
| 3 | Inspect the created Skill | The Skill's fields reflect the answers submitted in the clarification step |
| 4 | Check the chat response | A Skill chip/link is shown, reflecting the newly created Skill |

## Expected Final State

Missing Skill information triggers Ask User exactly once, and the submitted answers are used to complete the original creation request.

## Pass/Fail Criteria

**Pass:**
- Clarifying question card appears for missing required fields
- Skill created using the submitted answers
- Clarification card is not re-shown after submission

**Fail:**
- Assistant guesses missing fields without asking
- Skill fields do not reflect the submitted answers
- The clarification card reappears after submission
