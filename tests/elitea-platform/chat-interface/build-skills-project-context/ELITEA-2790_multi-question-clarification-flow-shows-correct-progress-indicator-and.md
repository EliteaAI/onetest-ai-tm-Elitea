---
id: ELITEA-2790
title: "Multi-question clarification flow shows correct progress indicator and Back/Next/Submit navigation"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, ask-user, clarifying-question-ui]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2790: Multi-question clarification flow shows correct progress indicator and Back/Next/Submit navigation

## Preconditions

- User is logged in to `{{base_url}}`
- Project Context Builder and Ask User are enabled

## Test Data

| Field | Value |
|-------|-------|
| Clarification flow | 3 required questions triggered by an ambiguous Project Context request |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a 3-question clarification flow | Progress indicator shows "Question 1 of 3"; only "Next" is available (no "Submit") |
| 2 | Leave question 1 unanswered and attempt to click Next | "Next" is disabled until the question is answered |
| 3 | Answer question 1 and click Next | Progress indicator updates to "Question 2 of 3"; "Back" is now available |
| 4 | Click Back | Returns to question 1 with the previously entered answer still populated |
| 5 | Navigate forward again to question 3 (final question) | Progress indicator shows "Question 3 of 3"; "Submit" is shown instead of "Next" |
| 6 | Click Submit | The flow completes and the original Project Context request resumes |

## Expected Final State

Progress indication and Back/Next/Submit controls behave correctly throughout a multi-question flow, and no answers are lost when navigating back and forth.

## Pass/Fail Criteria

**Pass:**
- Progress indicator accurate at every step
- Next disabled until required question answered
- Back preserves previously entered answers
- Submit shown only on the final question and completes the flow

**Fail:**
- Progress indicator incorrect or missing
- Next enabled before a required question is answered
- Back loses previously entered answers
- Submit is missing on the final question or shown earlier than the final question
