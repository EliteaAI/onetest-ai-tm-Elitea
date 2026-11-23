---
id: ELITEA-4792
title: "Save As Version keeps module changes on the new version and leaves the base version unchanged"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents, nfr:ui, modules, versioning, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4792: Save As Version keeps module changes on the new version and leaves the base version unchanged

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that module changes made in the "+ Modules" dropdown are stored on a version created with Save As Version, while the base version keeps its original module states.

## Preconditions

- Logged in to `{{base_url}}`
- An editable Agent exists on its base version
- Browser: Chrome (latest)

## Test Data

| Field | Value |
|---|---|
| Version name | `modules-reg-v2` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent (base version), click "+ Modules" and note every module state | Base states are recorded |
| 2 | Switch two modules to the opposite state | Switches change |
| 3 | Click Save As Version, enter `modules-reg-v2` and confirm | New version `modules-reg-v2` is created and opened |
| 4 | Click "+ Modules" | The two modules show the changed states; other modules match the base version |
| 5 | Switch the version selector to base and click "+ Modules" | All modules show the states recorded in step 1 |
| 6 | Switch back to `modules-reg-v2` and click "+ Modules" | The two changed states are still shown |

## Expected Final State

Each version keeps its own module configuration.

## Pass/Fail Criteria

**Pass:**
- New version has the changed module states and base version is unchanged

**Fail:**
- New version misses the changes, or base version module states are modified

## Notes

**Source functional tests:** ELITEA-4784
**Regression rationale:** Versioning is a core agent workflow; module state leaking between versions would break published agents.
**Selected checkpoints:** Changes on new version; base unchanged; stable after switching versions.
