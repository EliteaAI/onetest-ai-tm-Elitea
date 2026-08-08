---
id: ELITEA-1906
title: "Build with AI — agent draft is generated from a natural-language description"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_build_with_ai.TestAgentBuildWithAIDraftFieldPopulation.test_draft_fields_prepopulated_and_editable
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1319
---

# ELITEA-1906: Build with AI — agent draft is generated from a natural-language description

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that submitting a natural-language description in the GenerateAgentModal produces a complete, editable agent draft pre-populated with all required fields.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The GenerateAgentModal is accessible from the New Agent creation page.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language description | "An agent that helps write concise JIRA ticket descriptions" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GenerateAgentModal from the New Agent creation page | The modal opens with a prompt input field |
| 2 | Enter a natural-language description (e.g., "An agent that helps write concise JIRA ticket descriptions") | The input field accepts and displays the entered text |
| 3 | Click "Generate agent" | The modal shows a loading state while generation is in progress |
| 4 | Wait for generation to complete | The loading state ends and the modal transitions to the review/edit form |
| 5 | Verify the modal transitions to a review/edit form pre-populated with Name | The Name field is pre-populated with a generated value |
| 6 | Verify the review/edit form is pre-populated with Description | The Description field is pre-populated with a generated value |
| 7 | Verify the review/edit form is pre-populated with Instructions | The Instructions field is pre-populated with generated content |
| 8 | Verify the review/edit form is pre-populated with Welcome message | The Welcome message field is pre-populated with a generated value |
| 9 | Verify the review/edit form is pre-populated with Conversation starters | The Conversation starters field is pre-populated with generated suggestions |
| 10 | Verify all fields are editable before approval | All pre-populated fields can be edited by the user |

---

## Expected Final State

The GenerateAgentModal displays a fully populated review/edit form with Name, Description, Instructions, Welcome message, and Conversation starters — all editable before agent creation.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All required fields (Name, Description, Instructions, Welcome message, Conversation starters) are pre-populated and editable.

**Fail:**
- Any step produces an error or unexpected result.
- Any required field is missing, empty, or not editable in the review form.
