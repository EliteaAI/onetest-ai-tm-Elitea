---
id: ELITEA-0041
title: "Replace & Delete Migrates Dependent Entity and Removes Version — Agent & Pipeline [Parametrized]"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [nfr:usability, eng:frontend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5134]
---
# ELITEA-0041: Replace & Delete Migrates Dependent Entity and Removes Version — Agent & Pipeline [Parametrized]

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting a replacement version and clicking Replace & Delete migrates the dependent entity and permanently removes the in-use version.

**Coverage:**
- User can select a replacement version without the modal closing
- Replace & Delete button is clickable and completes the action
- Deleted version is removed from the version list
- Dependent entity references the chosen replacement version
- Covers both Agent and Pipeline entity types

## Preconditions

- Logged in to {{base_url}}
- **Variant A (Agent):** Agent A (3 versions: v1, v2, v3), Agent B uses v2 of Agent A
- **Variant B (Pipeline):** Pipeline P (3 versions: v1, v2, v3), Pipeline Q / Agent C uses v2 of Pipeline P
- Version deletion modal is open (trigger deletion of in-use v2)

## Test Data

| Variant | Entity | In-Use Version | Replacement | Dependent Entity |
|---|---|---|---|---|
| A | Agent A | v2 | v1 (or v3) | Agent B |
| B | Pipeline P | v2 | v1 (or v3) | Pipeline Q / Agent C |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the version deletion modal for the in-use version (v2) of the subject entity (Variant A or B). | Modal is open. Replacement versions (v1, v3) are listed. |
| 2 | Select a replacement version (e.g., v1) from the modal's version selector. | v1 is highlighted/selected. Modal remains open. |
| 3 | Click the Replace & Delete button. | Success indicator or confirmation message appears. Modal closes. |
| 4 | Check the subject entity's version list. | v2 is no longer listed. |
| 5 | Check the dependent entity's configured version reference. | Dependent entity now references v1 (the selected replacement). |
| 6 | Repeat steps 1–5 for the other entity variant. | Replace & Delete works correctly for both Agent and Pipeline. |

## Expected Final State

Replace & Delete works correctly for both Agent and Pipeline.

## Pass/Fail Criteria

**Pass:**
- Replacement version can be selected without the modal closing
- Replace & Delete button completes the action
- v2 is deleted and absent from the version list
- Dependent entity is migrated to the replacement version
- Success feedback is visible

**Fail:**
- Modal auto-closes before Replace & Delete can be clicked
- v2 is not deleted after the action
- Dependent entity still references v2
- Error is shown or action fails silently
