---
id: ELITEA-0556
title: "Verify Chipset Displays Subagent/Subpipeline Name Correctly When It Contains Spaces"
priority: high
type: functional
module: chipset-display
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend]
requirements: [ProjectAlita/projectalita.github.io#3782]
---
# ELITEA-0556: Verify Chipset Displays Subagent/Subpipeline Name Correctly When It Contains Spaces

**Module:** Chipset Display · **Priority:** High · **Type:** Functional

**Objective:** Verify that the chipset correctly displays a subagent or subpipeline name containing spaces exactly once, without duplication or concatenation.

**Coverage:**
- Name with spaces (e.g., "Chipset Space Test Agent") displayed once in the chipset after a run
- Name without spaces as a regression check — no duplication
- Name with multiple spaces displayed exactly once
- Subpipeline with a spaced name behaves identically to subagent

## Preconditions

- Logged in to {{base_url}}
- Browser: Chrome (latest)
- User has permission to create and run agents and pipelines
- A project is accessible and a parent agent/pipeline can be created or already exists

## Test Data

| Variation | Name Used | Type | Purpose |
|---|---|---|---|
| 1 — with spaces | Chipset Space Test Agent | Subagent | Main bug scenario: name with spaces |
| 2 — multiple spaces | Chipset Multi Space Test Agent | Subagent | Edge case: more than one space in name |
| 3 — subpipeline | Chipset Space Test Pipeline | Subpipeline | Same bug verified on pipeline type |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents section. Create a new subagent named 'Chipset Space Test Agent' (name contains spaces). | Subagent 'Chipset Space Test Agent' is created successfully. |
| 2 | Create or open a parent agent. Attach the subagent 'Chipset Space Test Agent' to it. Save the configuration. | Subagent is attached and the parent agent configuration is saved without errors. |
| 3 | Run the parent agent to trigger execution of the subagent. Wait for the run to complete. | Run completes without errors. |
| 4 | Observe the chipset output in the UI for the executed subagent 'Chipset Space Test Agent'. | Chipset displays the name exactly once in a clear format — e.g., 'Chipset Space Test Agent' or 'Chipset Space Test Agent (Chipset Space Test Agent)'. The format 'Chipset Space Test Agent: ChipsetSpaceTestAgent (Chipset Space Test Agent)' must NOT appear. |
| 5 | Repeat steps 1–4 using the name 'Chipset Multi Space Test Agent' (multiple spaces) as the subagent name. | Chipset displays 'Chipset Multi Space Test Agent' exactly once. No duplication or unexpected format. |
| 6 | Repeat steps 1–4 using a subpipeline named 'Chipset Space Test Pipeline' instead of a subagent. | Chipset displays 'Chipset Space Test Pipeline' exactly once. No duplication or unexpected format. |

## Expected Final State

Chipset displays 'Chipset Space Test Pipeline' exactly once. No duplication or unexpected format.

## Pass/Fail Criteria

**Pass:**
- Chipset displays the spaced name exactly once in all variations
- Name with multiple spaces displays exactly once
- Subpipeline with spaced name displays exactly once

**Fail:**
- Chipset shows the name duplicated or in a combined format (e.g., 'Chipset Space Test Agent: ChipsetSpaceTestAgent (Chipset Space Test Agent)')
- Name appears more than once in any variation
- Subagent/subpipeline without spaces exhibit unexpected duplication after the fix
