---
id: ELITEA-2755
title: "AI draft generation completes successfully with loading state displayed"
priority: critical
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

## Test Data

| Field | Value |
|-------|-------|
| Prompt | "Make this agent more professional and add error handling instructions" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent's configuration page as Editor/Admin | Page loads with current field values |
| 2 | Click "Edit with AI" CTA to open the modal | The modal opens at the prompt entry step |
| 3 | Enter the test prompt into the "Enter prompt" field | The typed text is reflected in the input |
| 4 | Click "Generate Draft" | AI processing starts |
| 5 | Observe the modal immediately after submission | A loading state is displayed showing "Generating agent draft…" with a spinner; the UI is non-interactive during generation |
| 6 | Wait for generation to complete | The loading state disappears once processing finishes |
| 7 | Observe the resulting view | The wizard displays with AI-generated suggestions for the relevant fields, replacing the loading state |

## Expected Final State

The wizard is displayed with populated suggestions derived from the submitted prompt; no changes have yet been applied to the Agent.

## Pass/Fail Criteria

**Pass:**
- Loading state with spinner and "Generating agent draft…" text appears immediately after submission and disappears once the wizard is ready
- The wizard renders with suggestions relevant to the prompt

**Fail:**
- No loading indicator is shown, generation hangs indefinitely, or the wizard fails to render after completion
