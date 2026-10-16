---
id: ELITEA-4063
title: "Selecting a shared model that has the same name as a project model runs and budgets the shared one"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, budget, shared-models, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6999", "EliteaAI/elitea_issues#7002"]
---

# ELITEA-4063: Selecting a shared model that has the same name as a project model runs and budgets the shared one

**Module:** analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a project model and a shared model have the same name, the one the user selected is the one that runs, and only the shared one counts against the budget.

---

## Preconditions

- A shared model available to the project.
- A project-own model configuration with exactly the same Model Name.
- Access to the user and project budget views (`user_budgets`, project `usage?scope=project`).

---

## Test Data

| Field | Value |
|-------|-------|
| Pair | Own and shared model with an identical Model Name |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Record the project budget usage for that model name and the user's budget spend. | Baseline. |
| 2 | Select the **shared** model in the agent and run once. | The call runs on the shared model (where visible: the shared project's LiteLLM model group). |
| 3 | Check the budget. | +1 request and +the run's cost for that model; the user's spend increases by the same amount. |
| 4 | Select the **own** model and run once. | The call runs on the own model. |
| 5 | Check the budget again. | No change: own models are metered but never budgeted. |
| 6 | Check how Analytics shows the two runs. | Record whether the two can be told apart (#7002). |

---

## Expected Final State

The selected model runs, and budgets count only the shared one.

---

## Pass/Fail Criteria

**Pass:**
- Shared selection runs on the shared model and is budgeted; own selection runs on the own model and is not.

**Fail:**
- The shared selection runs on the own model, or budgets count the own model.
