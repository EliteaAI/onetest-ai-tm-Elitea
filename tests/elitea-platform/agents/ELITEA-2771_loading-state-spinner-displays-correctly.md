---
id: ELITEA-2771
title: "Loading state spinner displays correctly during AI draft generation"
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

## Test Data

| Field | Value |
|-------|-------|
| Prompt | Any valid prompt, e.g. "Improve this agent" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Edit with AI modal and enter a prompt | Prompt accepted |
| 2 | Click "Generate Draft" | Generation request is submitted |
| 3 | Immediately observe the modal | "Generating agent draft…" message is displayed |
| 4 | Observe the loading indicator | A spinner animation is visible |
| 5 | Attempt to interact with other UI elements (e.g. navigate steps, close via background click) during generation | The UI is non-interactive; navigation away is blocked while generation is in progress |
| 6 | Wait for generation to complete | The loading state is replaced by the wizard once generation finishes |

## Expected Final State

The loading state renders correctly with message and spinner for the full duration of generation, blocking navigation, and cleanly transitions to the wizard on completion.

## Pass/Fail Criteria

**Pass:**
- Loading message and spinner display throughout generation; UI is non-interactive; transition to wizard is clean

**Fail:**
- No spinner/message shown, UI remains interactive during generation, or the loading state does not transition to the wizard
