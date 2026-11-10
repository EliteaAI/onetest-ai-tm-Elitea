---
id: ELITEA-2361
title: "Catalog — started conversation has agent added as participant"
priority: medium
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
---

# ELITEA-2361: Catalog — started conversation has agent added as participant

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Catalog — started conversation has agent added as participant. Success is confirmed when verify adent's avatar is visible in participants section.

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
| 1 | Navigate to Catalog (the Agents tab is active) | Catalog loads on the Agents tab (selected). |
| 2 | Click on an agent card (e.g., "User Story Creator") to open the detail modal | Control responds; expected next state is shown. |
| 3 | Click "Start conversation" | Control responds; expected next state is shown. |
| 4 | In the new chat, open the Participants panel on the right side | Action completes without error and produces the expected UI state. |
| 5 | Verify the agent appears under the AGENTS section of the participants list | Condition holds as described. |
| 6 | Verify the agent name matches the selected agent (e.g., "User Story Creator") | Condition holds as described. |
| 7 | Verify the agent version is displayed (e.g., "ver-0.1") | Condition holds as described. |
| 8 | Verify adent's avatar is visible in Participants section | Condition holds as described. |

---

## Expected Final State

Verify adent's avatar is visible in Participants section.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Catalog — started conversation has agent added as participant.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
