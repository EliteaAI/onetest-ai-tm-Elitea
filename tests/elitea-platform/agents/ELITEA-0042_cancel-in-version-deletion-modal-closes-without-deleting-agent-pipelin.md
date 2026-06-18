---
id: ELITEA-0042
title: "Cancel in Version Deletion Modal Closes Without Deleting — Agent & Pipeline [Parametrized]"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [nfr:usability, eng:frontend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5134]
---
# ELITEA-0042: Cancel in Version Deletion Modal Closes Without Deleting — Agent & Pipeline [Parametrized]

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking Cancel in the version deletion modal closes it without deleting the version or changing the dependent entity's configuration.

**Coverage:**
- Cancel button closes the modal
- In-use version is NOT deleted after Cancel
- Dependent entity still references the original version
- Covers both Agent and Pipeline entity types

## Preconditions

- Logged in to {{base_url}}
- **Variant A (Agent):** Agent A (3 versions), Agent B uses v2 of Agent A
- **Variant B (Pipeline):** Pipeline P (3 versions), Pipeline Q / Agent C uses v2 of Pipeline P
- Version deletion modal is open (trigger deletion of in-use v2)

## Test Data

| Variant | Entity | In-Use Version | Dependent Entity |
|---|---|---|---|
| A | Agent A | v2 | Agent B |
| B | Pipeline P | v2 | Pipeline Q / Agent C |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the version deletion modal for the in-use version (v2) of the subject entity (Variant A or B). | Modal is open and shows available replacement versions. |
| 2 | Click the Cancel button. | Modal closes. No success message or loading indicator appears. |
| 3 | Check the subject entity's version list. | v2 is still present — it was not deleted. |
| 4 | Check the dependent entity's configured version reference. | Still references v2. No migration occurred. |
| 5 | Repeat steps 1–4 for the other entity variant. | Cancel behavior is consistent for both Agent and Pipeline. |

## Expected Final State

Cancel behavior is consistent for both Agent and Pipeline.

## Pass/Fail Criteria

**Pass:**
- Modal closes on Cancel with no side effects
- Version v2 remains in the entity's version list
- Dependent entity's version reference is unchanged

**Fail:**
- Modal does not close after Cancel
- Version is deleted despite cancellation
- Dependent entity's version reference changes
