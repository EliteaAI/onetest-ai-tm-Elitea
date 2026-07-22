---
id: ELITEA-2416
title: "Chat throws a meaningful error when the assigned LLM model uses invalid credentials"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2416: Chat throws a meaningful error when the assigned LLM model uses invalid credentials

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Chat throws a meaningful error when the assigned LLM model uses invalid credentials. Success is confirmed when verify no raw stack trace or internal error details are exposed to the user.

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
| 1 | Navigate to Settings → Credentials and create a credential with an invalid API key | Target page/section loads successfully. |
| 2 | Navigate to Settings → AI Configuration → click "+" → create a new LLM model using the invalid credential | Target page/section loads successfully. |
| 3 | Save the LLM model configuration | Operation completes successfully; state updates and confirmation is shown. |
| 4 | Navigate to Agents and open or create an agent that uses the newly created invalid LLM model | Target page/section loads successfully. |
| 5 | Open a chat session with the agent | Target page/section loads successfully. |
| 6 | Send any message | Action completes without error and produces the expected UI state. |
| 7 | Verify the chat does not hang indefinitely or show a blank response | Condition holds as described. |
| 8 | Verify a user-friendly error message is displayed in the chat (e.g., "Model unavailable" or "Failed to get response") | Condition holds as described. |
| 9 | Verify no raw stack trace or internal error details are exposed to the user | Condition holds as described. |

---

## Expected Final State

Verify no raw stack trace or internal error details are exposed to the user.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat throws a meaningful error when the assigned LLM model uses invalid credentials.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
