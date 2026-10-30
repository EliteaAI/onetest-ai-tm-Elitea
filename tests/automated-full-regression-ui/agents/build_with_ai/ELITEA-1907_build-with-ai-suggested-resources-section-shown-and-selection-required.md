---
id: ELITEA-1907
title: "Build with AI — suggested resources section is shown and requires explicit selection"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1907: Build with AI — suggested resources section is shown and requires explicit selection

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that the generated agent draft includes a "Suggested Resources" section (Toolkits, Agents) and that these resources require explicit user selection before being attached to the created agent.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- At least one Toolkit exists in the project (e.g., GitHub toolkit).
- The GenerateAgentModal is accessible from the New Agent creation page.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language description | Agent description that matches existing project resources (e.g., "GitHub assistant") |
| Existing Toolkit | GitHub toolkit (pre-existing) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GenerateAgentModal and enter a natural-language description that matches existing resources | The description is entered successfully |
| 2 | Click "Generate agent" | The generation process starts and completes |
| 3 | Verify the review form displays a "Suggested Resources" section | The "Suggested Resources" section is visible in the review form |
| 4 | Verify the section includes suggested Toolkits and/or Agents (if relevant matches exist) | Relevant Toolkits and/or nested Agents are listed as suggestions |
| 5 | Verify that suggested resources are NOT pre-selected by default | All suggested resource cards are in an unselected state (not highlighted) |
| 6 | Verify that user must explicitly click a resource card to select it | Clicking a resource card highlights it as selected |
| 7 | Click "Approve" / "Create Agent" WITHOUT selecting any suggested resources | The agent creation is initiated |
| 8 | Open the created Agent and verify NO suggested resources were automatically attached | The agent's TOOLKITS/AGENTS sections are empty or contain only manually added resources, NOT the suggested ones |

---

## Expected Final State

The "Suggested Resources" section is displayed during agent draft review, resources are not pre-selected, and only explicitly selected resources are attached to the created agent.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The "Suggested Resources" section is visible and populated with relevant suggestions.
- Resources are not pre-selected by default.
- Only explicitly selected resources are attached to the created agent.

**Fail:**
- Any step produces an error or unexpected result.
- The "Suggested Resources" section is missing.
- Resources are pre-selected without user action.
- Non-selected resources are automatically attached to the agent.

---

## Notes

**Source functional tests:** ELITEA-1907 (original), ELITEA-1908 (original)  
**Regression rationale:** Consolidated test verifying both the presence of the Suggested Resources section and the explicit selection requirement. Both assertions are tightly coupled aspects of the same feature behavior.  
**Selected checkpoints:** Section visibility, default unselected state, selection interaction, attachment outcome.
