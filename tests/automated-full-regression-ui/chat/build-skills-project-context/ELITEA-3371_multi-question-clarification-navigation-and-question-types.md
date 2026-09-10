---
id: ELITEA-3371
title: "Multi-question clarification flow navigation, progress indicator, and question types"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, story:6239, regression, ask-user, clarifying-question, navigation]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3371: Multi-question clarification flow navigation, progress indicator, and question types

## Objective

Verify that multi-question clarification flows display correct progress indicator, Back/Next/Submit navigation works correctly, all question types (single-select, multi-select, free-text, Other option) are supported, and optional questions do not block progression.

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder and Ask User are enabled in Chat Modules

## Test Data

| Field | Value |
|-------|-------|
| Trigger request | An ambiguous Skill creation request that triggers 3+ questions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send an ambiguous Skill creation request that triggers multiple clarifying questions | A clarifying-question card appears; progress indicator shows "Question 1 of N" |
| 2 | Verify only "Next" is available on question 1 (not "Submit") | "Next" button is visible; "Submit" is not shown; "Back" is not available on first question |
| 3 | Leave question 1 unanswered and attempt to click Next | "Next" button is disabled until required question is answered |
| 4 | Answer question 1 (if single-select, select one option) | Answer is recorded |
| 5 | If "Other" option exists, select it and enter custom text | Custom text input is accepted as the answer |
| 6 | Click Next | Progress indicator updates to "Question 2 of N"; "Back" is now available |
| 7 | Click Back | Returns to question 1; previously entered answer is still populated |
| 8 | Navigate forward again to question 2 | Question 2 is displayed |
| 9 | If question 2 is multi-select, select two or more options | Multiple selections are retained simultaneously |
| 10 | Continue to last question (question N) | Progress indicator shows "Question N of N"; "Submit" is shown instead of "Next" |
| 11 | If last question is optional, verify Next/Submit remains enabled without answering | Optional question does not block progression |
| 12 | If last question is free-text, enter a description | Free-text input is accepted |
| 13 | Click Submit | The flow completes; clarification card closes; original Skill creation resumes |
| 14 | Verify Skill is created with all submitted answers | Skill fields reflect all answers including custom "Other" value and multiple selections |

## Expected Final State

Progress indication and Back/Next/Submit controls work correctly throughout the flow, all question types are supported, answers are preserved when navigating, optional questions don't block, and final Skill reflects all submitted answers.

## Pass/Fail Criteria

**Pass:**
- Progress indicator accurate at every step (e.g., "Question 1 of 3")
- Next disabled until required question answered
- Back preserves previously entered answers
- Submit shown only on the final question
- Single-select, multi-select, free-text all render and accept input correctly
- "Other" option with custom text is accepted and used
- Multi-select retains multiple choices
- Optional questions allow skipping without blocking
- Final Skill reflects all submitted answers

**Fail:**
- Progress indicator incorrect or missing
- Next enabled before required question is answered
- Back loses previously entered answers
- Submit shown before final question or missing on final question
- Any question type fails to render or accept input
- "Other" value or multi-select choices are lost
- Optional question blocks progression
