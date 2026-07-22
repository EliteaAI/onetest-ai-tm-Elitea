---
id: ELITEA-2417
title: "AI Credentials section is hidden when no credentials are configured"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2417: AI Credentials section is hidden when no credentials are configured

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that AI Credentials section is hidden when no credentials are configured. Success is confirmed when verify the ai credentials section now appears with the newly created credential card.

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
| 1 | Navigate to Settings → AI Configuration in a project with no AI credentials configured | Target page/section loads successfully. |
| 2 | Verify the AI Credentials section is NOT shown in the page | Condition holds as described. |
| 3 | Add a new credential via "+" → "AI Credentials" | Operation completes successfully; state updates and confirmation is shown. |
| 4 | Complete and save the credential | Action completes without error and produces the expected UI state. |
| 5 | Verify the AI Credentials section now appears with the newly created credential card | Condition holds as described. |

---

## Expected Final State

Verify the AI Credentials section now appears with the newly created credential card.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: AI Credentials section is hidden when no credentials are configured.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
