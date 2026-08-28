---
id: ELITEA-2388
title: "Default Personality change applies to new conversations"
priority: medium
type: functional
module: settings-user-profile
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_personalization_new_conversations_only.TestPersonalizationAppliesToNewConversationsOnly.test_personalization_applies_to_new_conversations_only
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1969"
---

# ELITEA-2388: Default Personality change applies to new conversations

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Default Personality change applies to new conversations. Success is confirmed when verify the existing conversation personality setting is unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Personalization → GENERAL | Target page/section loads successfully. |
| 2 | Set Default Personality to "Nerdy" | Action completes without error and produces the expected UI state. |
| 3 | Navigate away and back to confirm the value was auto-saved | Target page/section loads successfully. |
| 4 | Create a new conversation | Operation completes successfully; state updates and confirmation is shown. |
| 5 | Verify the new conversation uses the "Nerdy" personality setting | Condition holds as described. |
| 6 | Open a previously existing conversation | Target page/section loads successfully. |
| 7 | Verify the existing conversation personality setting is unchanged | Condition holds as described. |

---

## Expected Final State

Verify the existing conversation personality setting is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Default Personality change applies to new conversations.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
