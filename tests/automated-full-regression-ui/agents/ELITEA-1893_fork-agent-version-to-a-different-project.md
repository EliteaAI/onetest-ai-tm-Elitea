---
id: ELITEA-1893
title: "Fork agent version to a different project"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1893: Fork agent version to a different project

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that an agent version can be forked to a different project, that the fork wizard displays entity cards correctly, and that the forked agent in the target project matches the source version's configuration.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least two projects are accessible to the user.
- An existing agent with a version to fork is available in the current project.

---

## Test Data

| Field | Value |
|-------|-------|
| Target project | A different project from the current one |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page and select the version to fork | The desired version is active |
| 2 | Click the three-dot menu (⋮) → select "Fork" | The Fork wizard opens |
| 3 | Verify the Fork wizard opens | The Fork wizard dialog is displayed |
| 4 | Select a target project DIFFERENT from the current project | The target project is selected |
| 5 | Verify entity cards show the main agent (and any nested dependencies) | Entity cards for the agent and all dependencies are visible |
| 6 | Click Fork | The fork operation is initiated |
| 7 | Click "Got it" — verify navigation to the forked agent in the target project | The user is navigated to the forked agent in the target project |
| 8 | Verify the forked agent has matching instructions and configuration to the source version | The forked agent's instructions and configuration match the source |
| 9 | Clean up: delete the forked agent from the target project | The forked agent is deleted successfully |

---

## Expected Final State

The forked agent exists in the target project with instructions and configuration matching the source version. Cleanup is performed after verification.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The forked agent is created in the target project with matching configuration.

**Fail:**
- Any step produces an error or unexpected result.
- The fork fails, navigates to the wrong project, or the forked agent has incorrect configuration.
