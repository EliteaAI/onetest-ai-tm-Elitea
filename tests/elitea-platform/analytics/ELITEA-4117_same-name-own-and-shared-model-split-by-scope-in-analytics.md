---
id: ELITEA-4117
title: "A model name used as both a project-own and a shared model shows as two rows, one per scope, in analytics"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, shared-models, issue:7002, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7002"]
---

# ELITEA-4117: A model name used as both a project-own and a shared model shows as two rows, one per scope, in analytics

**Module:** analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that analytics no longer merges calls when a project's own model has the same name as a shared model. Every view that lists models must show one row per scope, with `model_scope` (`own` / `shared`) and a display name ending in ` (project)` or ` (shared)`. Calls and cost are counted for each row separately. Models used under only one scope keep their plain name.

**Out of scope:** routing and budgeting of the pair (ELITEA-4063, #6999); Run detail, Agents "model used" and Tools detail (not changed by the fix, see ELITEA-4118).

---

## Preconditions

- #6999 is fixed. Scope comes from `budget_exempt`, which the proxy sets to TRUE only when the project's own deployment served the call.
- A shared model from the public project is available to project **P** (e.g. `gpt-5.6-luna-2026-07-09`, display name "Dial-GPT-5.6-Luna").
- In P, an **own** LLM config with exactly the same Model Name. Give it a **different** display name (e.g. "Luna Own"), so you can check that each scope keeps its own display name.
- An agent **A** in P, and a skill **S** in P that makes an LLM call.
- Another model **M2** that P uses under one scope only.
- Rights to read Settings → Analytics and the analytics API for P.

---

## Test Data

| Field | Value |
|-------|-------|
| Shared model | `gpt-5.6-luna-2026-07-09`, display "Dial-GPT-5.6-Luna" |
| Own model | same Model Name, display "Luna Own" |
| Prompt | "Reply with exactly: OK 7002 shared" / "… own" |
| Runs | shared ×2, own ×1 (so the counts differ) |

---

## Steps

### Part A: Generate usage

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Record the baseline from `analytics_costs` → `by_model` for today. | Baseline calls and `total_cost` per row. |
| 2 | Set agent A to the **shared** model and run it twice. Set A to the **own** model and run it once. Run A once on M2. | Every run answers correctly. Note the run IDs. |
| 3 | Run skill S once on the shared model and once on the own model. | Both runs succeed. |

### Part B: API views

| # | Action | Expected Result |
|---|--------|-----------------|
| 4 | GET `analytics_costs`, read `by_model`. | **Two** rows for the model name. Row `model_scope: shared` has display "Dial-GPT-5.6-Luna (shared)" and +2 calls. Row `model_scope: own` has display "Luna Own (project)" and +1 call. |
| 5 | In the same response, compare `total_cost` for the two rows with the run costs from step 2. | Each row's cost increase equals its own runs' cost. Cost isn't merged into one row. |
| 6 | GET `analytics`, read `models`. | Same two rows, with the same counts and labels as step 4. Each row has `model_scope`. |
| 7 | GET `analytics_user_detail` for the user who ran the agent, and read `models`. | Same two rows and labels. |
| 8 | GET skill detail for S. Read `by_model` and `recent_runs`. | `by_model` has an `own` row "Luna Own (project)" and a `shared` row "Dial-GPT-5.6-Luna (shared)". In `recent_runs`, each run shows the label for its own scope. |
| 9 | In all the responses above, check M2 and every other model. | No suffix. The plain display name is shown. |
| 10 | GET `/usage?scope=project`. | Only the shared row is listed, "Dial-GPT-5.6-Luna (shared)". Own models are never budgeted. Cross-check only: budgets are covered in ELITEA-4063. |

### Part C: UI

| # | Action | Expected Result |
|---|--------|-----------------|
| 11 | Open Settings → Analytics → Overview, then the models table. | Two rows, "Dial-GPT-5.6-Luna (shared)" and "Luna Own (project)", with the counts from step 4. |
| 12 | Open the Costs tab, then the by-model chart and table. | Same two labels and separate costs. Neither row shows the raw model name. |
| 13 | Open the user detail page and the skill detail page from steps 7 and 8. | The labels match the API. |

---

## Expected Final State

Each scope has its own row, label and totals in every analytics view the fix changed. Models used under a single scope look the same as before.

---

## Pass/Fail Criteria

**Pass:**
- Costs by model, Overview models, User detail and Skill detail each show two rows, and each row has `model_scope` and its suffix.
- Each scope keeps its own display name, calls and cost.
- Models used under a single scope have no suffix.
- The UI shows the qualified labels.

**Fail:**
- The two scopes are merged into one row, or both rows have the same label.
- Calls or cost are counted under the wrong scope.
- A suffix appears on a model that is used under only one scope.
