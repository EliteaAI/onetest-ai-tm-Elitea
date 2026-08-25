---
id: ELITEA-2775
title: "Generation failure displays error message and allows retry"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent's configuration page is open
- A method to induce or simulate AI generation failure is available (e.g. network throttling/blocking the generation request, or an environment condition known to cause failure)

## Test Data

| Field | Value |
|-------|-------|
| Prompt | Any valid prompt, e.g. "Improve this agent" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Edit with AI modal and enter a prompt | Prompt accepted |
| 2 | Induce a generation failure (e.g. block/interrupt the generation network request) and click "Generate Draft" | Generation is attempted and fails |
| 3 | Observe the modal after failure | An error message is displayed explaining the generation failed |
| 4 | Verify a retry option/button is available | Retry control is present |
| 5 | Remove the induced failure condition and click retry | A new generation attempt is triggered |
| 6 | Wait for the retried generation to complete | Generation succeeds and the wizard is displayed normally |

## Expected Final State

On failure, the user sees a clear error message and can retry without needing to close and reopen the modal; a successful retry proceeds normally to the wizard.

## Pass/Fail Criteria

**Pass:**
- A clear error message appears on failure, and retry successfully re-attempts generation

**Fail:**
- No error message is shown, the modal becomes stuck/unresponsive, or no retry path is available
