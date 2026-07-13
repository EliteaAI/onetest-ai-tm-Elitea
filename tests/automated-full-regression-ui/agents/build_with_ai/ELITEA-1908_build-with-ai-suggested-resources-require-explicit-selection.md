---
id: ELITEA-1908
title: "Build with AI — suggested resources require explicit selection before creation"
priority: medium
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1908: Build with AI — suggested resources require explicit selection before creation

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that suggested resources (Toolkits, Agents, Pipelines, MCPs) in the review form are not automatically attached to the created agent — only explicitly selected resources are linked.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The GenerateAgentModal produces a draft with Suggested Resources.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate an agent draft that includes suggested Toolkits and/or Agents | The review form is displayed with a Suggested Resources section |
| 2 | In the review form, do NOT select any suggested resources | All suggested resource cards remain in unselected state |
| 3 | Click "Approve" / "Create Agent" | The agent creation is initiated |
| 4 | Open the created Agent | The Agent detail page is displayed |
| 5 | Verify no Toolkits, Agents, Pipelines, or MCPs were automatically attached | No resources appear in the Toolkits, Agents, Pipelines, or MCPs sections of the created agent |

---

## Expected Final State

The created agent has no Toolkits, Agents, Pipelines, or MCPs attached, confirming that skipping selection results in no auto-attached resources.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The created agent has no automatically attached resources when none were selected.

**Fail:**
- Any step produces an error or unexpected result.
- One or more suggested resources are automatically attached to the agent without explicit selection.
