---
id: ELITEA-1916
title: "Build with AI — creation failure stays on review step for correction (Agent)"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_build_with_ai.TestAgentBuildWithAICreationFailureRecovery.test_creation_failure_stays_on_review_step_and_retry_succeeds
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1319
---

# ELITEA-1916: Build with AI — creation failure stays on review step for correction (Agent)

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that when agent creation fails after clicking Approve, the user remains on the review/edit step with all draft data intact, allowing them to correct the issue and resubmit.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- An agent draft has been generated and the review/edit form is displayed.
- A creation API failure condition can be triggered or simulated.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate an agent draft and click "Approve" / "Create Agent" | The creation request is submitted |
| 2 | Simulate or trigger a creation API failure | The creation API call fails |
| 3 | Verify form-level error messages are shown using the standard creation error handling | Error messages are displayed on the form indicating the creation failure |
| 4 | Verify the user remains on the review/edit step (not redirected or kicked to prompt step) | The user stays on the review/edit form; no unwanted navigation occurs |
| 5 | Verify all draft data (Name, Description, Instructions, selected resources) is still present | All previously entered and selected data is preserved on the form |
| 6 | Correct the issue and click "Approve" again — verify the Agent is created successfully | The agent is created successfully on the second attempt |

---

## Expected Final State

After a creation failure, the user remains on the review step with all data intact. After correcting the issue, the agent is created successfully.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Error messages are shown, user stays on review step, all data is preserved, and retry succeeds.

**Fail:**
- Any step produces an error or unexpected result.
- User is redirected away from review step on failure, or draft data is lost after a creation failure.
