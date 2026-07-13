---
id: ELITEA-1869
title: "Agent listing — back navigation from agent detail returns to Agents list"
priority: high
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1869: Agent listing — back navigation from agent detail returns to Agents list

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking the Back button on an agent detail page returns the user to the Agents dashboard with the list intact, without redirecting to an unrelated page.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one agent exists in the current project.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Agents page | The Agents dashboard loads and displays the list of agents |
| 2 | Click into any agent card to open its detail page | The agent detail page opens |
| 3 | Click the Back button in the agent detail page header | Navigation is triggered back to the previous page |
| 4 | Verify the Agents dashboard is shown | The Agents dashboard is visible |
| 5 | Verify the list is intact (not blank, not redirected to Chat or another page) | The agents list is fully rendered with all previously visible agents |

---

## Expected Final State

The user is back on the Agents dashboard with the agent list fully visible and intact, not redirected to Chat or any other page.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The Back button returns the user to the Agents dashboard with the list intact.

**Fail:**
- Any step produces an error or unexpected result.
- The user is redirected to a page other than the Agents dashboard, or the list appears blank.
