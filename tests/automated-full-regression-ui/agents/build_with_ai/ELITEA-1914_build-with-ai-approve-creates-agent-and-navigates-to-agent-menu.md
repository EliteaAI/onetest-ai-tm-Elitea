---
id: ELITEA-1914
title: "Build with AI — Approve creates the agent and navigates to Agent menu"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_build_with_ai.TestAgentBuildWithAISelectedResourcesAttached.test_approve_with_no_resources_creates_agent_and_appears_in_list
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1319
---

# ELITEA-1914: Build with AI — Approve creates the agent and navigates to Agent menu

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking "Approve" / "Create Agent" in the Build with AI review form creates the agent in the current project and navigates the user to the Agent detail/menu page, with the agent also visible in the Agents list.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- An agent draft has been generated and the review/edit form is displayed.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate an agent draft, optionally edit fields, and select desired resources | The review form reflects the finalized agent configuration |
| 2 | Click "Approve" / "Create Agent" | The agent creation request is submitted |
| 3 | Verify the agent is created in the current project | The agent is created successfully without errors |
| 4 | Verify the user is navigated to the created Agent (Agent menu / Agent details) | The user is redirected to the Agent detail/menu page for the newly created agent |
| 5 | Navigate to the Agents list and verify the new Agent appears there | The newly created agent is visible in the Agents list |

---

## Expected Final State

The agent is created in the current project, the user is on the Agent detail page, and the new agent appears in the Agents list.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The agent is created, the user is navigated to the Agent detail page, and the agent appears in the Agents list.

**Fail:**
- Any step produces an error or unexpected result.
- The agent is not created, navigation does not occur, or the agent is absent from the Agents list.
