---
id: ELITEA-0043
title: "Version Deletion Modal Stays Open on Any Click — Agent & Pipeline [Parametrized]"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [nfr:usability, eng:frontend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5134]
---
# ELITEA-0043: Version Deletion Modal Stays Open on Any Click — Agent & Pipeline [Parametrized]

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the version deletion modal does not auto-close when the user clicks inside it or selects a version, but does close when clicking outside — for both Agent and Pipeline entities.

**Coverage:**
- Modal appears when deleting an in-use Agent version
- Modal appears when deleting an in-use Pipeline version
- Modal does not auto-close on click inside the modal body
- Modal does not auto-close when selecting a replacement version
- Modal closes when clicking outside (overlay/background) — expected behavior

## Preconditions

- Logged in to {{base_url}}
- **Variant A (Agent):** Agent A exists with 3 versions (v1, v2, v3); Agent B uses v2 of Agent A as a sub-agent
- **Variant B (Pipeline):** Pipeline P exists with 3 versions (v1, v2, v3); Pipeline Q or Agent C uses v2 of Pipeline P

## Test Data

| Variant | Entity | In-Use Version | Dependent Entity |
|---|---|---|---|
| A | Agent A | v2 | Agent B |
| B | Pipeline P | v2 | Pipeline Q / Agent C |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the subject entity (Agent A for Variant A, Pipeline P for Variant B). Navigate to its versions list. | Versions list is displayed showing v1, v2, v3. |
| 2 | Attempt to delete v2 (the version currently in use). | A confirmation modal appears prompting the user to select a replacement version for migration. |
| 3 | Click anywhere inside the modal body (not on Cancel or Replace & Delete). | Modal remains open. No auto-close occurs. |
| 4 | Click on one of the available version options (e.g., v1 or v3) in the modal's version selector. | Selected version is highlighted. Modal remains open. |
| 5 | Click outside the modal on the dimmed overlay/background. | Modal closes. This is the expected behavior — clicking outside dismisses the modal. |
| 6 | Repeat steps 1–5 for the other entity variant. | Behavior is consistent for both Agent and Pipeline. |

## Expected Final State

Behavior is consistent for both Agent and Pipeline.

## Pass/Fail Criteria

**Pass:**
- Modal appears for both Agent and Pipeline in-use version deletion
- Modal does not auto-close on click inside the modal body
- Modal does not auto-close when selecting a version option
- Modal closes when clicking outside (overlay) — expected
- Behavior is consistent across both entity types

**Fail:**
- Modal auto-closes on click inside the modal body
- Modal auto-closes when the user selects a version option
- Modal does not appear when deleting an in-use version
- Modal does NOT close when clicking outside (overlay)
- Bug is fixed for one entity type but not the other
