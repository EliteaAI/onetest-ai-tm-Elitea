---
id: ELITEA-1703
title: "Artifacts Tool Behavior Not Affected by Guardrails Changes"
priority: high
type: regression
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:artifacts, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1703: Artifacts Tool Behavior Not Affected by Guardrails Changes

**Module:** Admin Portal / Guardrails · **Priority:** High · **Type:** Regression

**Objective:** Verify that the Artifacts tool behavior is not impacted by the case-insensitive matching and live-reload changes to Guardrails.

## Preconditions

- Logged in as a user with access to Artifacts functionality
- Agent configured with Artifacts capability
- Guardrails configured with some blocked/sensitive tools (not Artifacts)

## Test Data

| Artifact Type | Action to Test |
|--------------|----------------|
| Code snippet | Create, view, edit |
| Document | Create, view, edit |
| Image/diagram | Create, view |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open agent chat with Artifacts capability enabled. | Agent chat opens. Artifacts panel available. |
| 2 | Send prompt: "Create a Python code snippet that prints Hello World". | Agent creates an Artifact with Python code. |
| 3 | View the created Artifact. | Artifact displays correctly with syntax highlighting. |
| 4 | Ask agent to modify the artifact: "Add a loop that prints numbers 1-5". | Agent modifies the Artifact. Changes reflected. |
| 5 | Create a document artifact: "Create a markdown document outlining a project plan". | Document Artifact created successfully. |
| 6 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails page loads. |
| 7 | Add a random toolkit to Blocked Toolkits. Save. | Configuration saved with live reload. |
| 8 | Return to agent chat. Create another Artifact. | Artifacts still work normally. |
| 9 | Modify Guardrails again (add/remove sensitive tool). Save. | Configuration saved. |
| 10 | Verify Artifacts creation, viewing, and editing still function. | All Artifacts operations work as expected. |
| 11 | Test Artifact versioning if applicable. | Version history works correctly. |

## Expected Final State

Artifacts tool operates normally regardless of Guardrails configuration changes. The case-insensitive matching and live-reload changes have no impact on Artifacts functionality.

## Pass/Fail Criteria

**Pass:**
- Artifacts can be created after Guardrails changes
- Artifacts can be viewed after Guardrails changes
- Artifacts can be edited after Guardrails changes
- No unexpected authorization dialogs for Artifacts operations
- Artifacts are not inadvertently blocked by Guardrails
- Artifact versioning (if applicable) works correctly

**Fail:**
- Artifacts functionality broken after Guardrails changes
- Artifacts inadvertently blocked or marked as sensitive
- Artifacts tool affected by case-insensitive matching
- Live-reload breaks Artifacts capability
- Any Artifacts operation fails that previously worked
