---
id: ELITEA-4118
title: "Model scope labels hold up after the own config is deleted, inside the 'Other models' row, and on legacy rows"
priority: medium
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, shared-models, issue:7002, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7002"]
---

# ELITEA-4118: Model scope labels hold up after the own config is deleted, inside the "Other models" row, and on legacy rows

**Module:** analytics · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the edge cases of the #7002 scope split. Rows already recorded keep splitting by scope after the own config is deleted. Labels are resolved before the "Other models" tail is collapsed. Rows written before #6999 count as shared. The views the fix did not change are also checked and their current behaviour is recorded.

---

## Preconditions

- ELITEA-4117 was run in project **P**, so P has today's `own` and `shared` rows for the same model name. Note the run IDs.
- Rights to edit P's AI configurations.
- For step 6: P uses more models than the Costs by-model display limit, so an "Other models" row appears (see ELITEA-4061).
- For step 8: a project with usage rows from **before** the #6999 deploy for a name that is now also an own model.

---

## Steps

### Part A: Own config deleted

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Delete P's own config with the duplicate name. | Deleted. Only the shared config is left. |
| 2 | GET `analytics_costs` → `by_model` and `analytics` → `models` for today. | Still **two** rows. `own` reads "Dial-GPT-5.6-Luna (project)" (it borrows the shared display name) and `shared` reads "Dial-GPT-5.6-Luna (shared)". Counts are unchanged. |
| 3 | GET `/usage?scope=project`. | The model is shown with its plain display name and no suffix. The Usage page labels models from configs only. |
| 4 | Run agent A once more on the shared model, then repeat step 2. | The `shared` row goes up by 1. The `own` row stays the same. |
| 5 | Pick a date range that has no own-scope calls. | One row with the plain name and no suffix. |

### Part B: "Other models" and legacy rows

| # | Action | Expected Result |
|---|--------|-----------------|
| 6 | With more models than the display limit, GET `analytics_costs` → `by_model`. | The rows above the limit are labelled correctly per scope, even when only one of the pair is in the top list. The collapsed row reads "Other models". |
| 7 | Change the range so that both rows of the pair are in the top list. | Both rows are shown, each with its suffix. |
| 8 | In the project with pre-#6999 rows, open Costs for a range that covers them. | Those rows count under `shared`. This is a known limitation: older rows can't be reclassified. |

### Part C: Views the fix didn't change (record only)

| # | Action | Expected Result |
|---|--------|-----------------|
| 9 | GET `analytics_run_detail` for an own run and a shared run from ELITEA-4117. | **Known gap:** each `llm_calls` item has `model_name` and no `model_scope`. Record the result and link it to a follow-up enhancement. It isn't a #7002 failure. |
| 10 | Open Analytics → Agents for agent A ("model used"). Then open Tools detail. | Record whether the two scopes can be told apart. If they can't, add it to the same follow-up. |

### Cleanup

| # | Action | Expected Result |
|---|--------|-----------------|
| 11 | Set agent A back to its original model. Recreate the own config only if another test needs it. | P is back in its original state. |

---

## Expected Final State

The scope split survives deleting the own config, and it works around the "Other models" collapse. Legacy rows count as shared. The views the fix didn't change are recorded.

---

## Pass/Fail Criteria

**Pass:**
- Steps 2 to 8 behave as described.

**Fail:**
- After the config is deleted, the rows merge or have identical labels.
- A suffix appears on a range that has only one scope.
- Labels are wrong inside or next to the "Other models" row.
- Steps 9 and 10 are informational. They don't fail this test.
