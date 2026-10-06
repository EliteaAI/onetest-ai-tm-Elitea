---
id: ELITEA-2425
title: "Assistant receives current page context"
priority: medium
type: functional
module: support-assistant
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-2425: Assistant receives current page context

**Module:** support-assistant · **Priority:** medium · **Type:** functional

**Objective:** Verify that Assistant receives current page context. Success is confirmed when open a specific agent detail page; send: "what entity am i currently viewing?" — verify the assistant reports the agent name/type from the context payload.

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
| 1 | Navigate to the Agents page (URL path: /agents/all or similar) | Target page/section loads successfully. |
| 2 | Open the Support Assistant widget | Target page/section loads successfully. |
| 3 | Send: "What page am I currently on in the application?" | Action completes without error and produces the expected UI state. |
| 4 | Verify the assistant responds with a reference to the Agents section or the correct current page path | Condition holds as described. |
| 5 | Navigate to the Pipelines page and open the widget again | Target page/section loads successfully. |
| 6 | Send the same question — verify the assistant now reports the Pipelines page context | Action completes without error and produces the expected UI state. |
| 7 | Open a specific Agent detail page; send: "What entity am I currently viewing?" — verify the assistant reports the agent name/type from the context payload | Target page/section loads successfully. |

---

## Expected Final State

Open a specific Agent detail page; send: "What entity am I currently viewing?" — verify the assistant reports the agent name/type from the context payload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Assistant receives current page context.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
