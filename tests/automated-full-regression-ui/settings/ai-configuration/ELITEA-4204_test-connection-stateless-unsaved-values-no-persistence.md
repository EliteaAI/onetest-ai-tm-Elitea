---
id: ELITEA-4204
title: "Test connection evaluates unsaved form values and has no persistence side effects"
priority: critical
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

## Preconditions

- User is logged in to `{{base_url}}` as a project admin.
- An existing saved LLM model configuration exists that the tester can edit.
- Project has at least one valid AI credential.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Existing Model | A saved LLM model configuration available for editing |
| New Valid Model Name | Different valid identifier than the currently saved one |
| New Invalid Model Name | Misspelled/non-existent identifier |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Part 1: Test connection evaluates unsaved form values** |
| 1 | Note current LLM model configuration list (baseline) | Baseline recorded. |
| 2 | Open existing configuration for editing | Form loads with saved values. |
| 3 | Change Model Name to a different valid value, don't save | Recognition indicator updates to "Recognized" for new value. |
| 4 | Click Test connection | Spinner shown; result returned. |
| 5 | Observe result | Result reflects the new unsaved value (success, "Connected in N s"), consistent with recognition indicator. |
| 6 | Change Model Name to an invalid value, don't save | Recognition indicator updates to "Not recognized" for new value. |
| 7 | Click Test connection again | Spinner shown; result returned. |
| 8 | Observe result | Result reflects the latest unsaved value (e.g., "Model not found"), consistent with recognition indicator. |
| **Part 2: Test connection has no persistence side effects** |
| 9 | Without saving, navigate away or reload the page | Page navigates/reloads. |
| 10 | Review model configuration list | No new or altered model in the list compared to baseline (step 1). |
| 11 | Open the same model configuration for editing | Form loads with original saved values (not the unsaved test values from steps 3 or 6). |

## Expected Final State

Test connection always reflects current unsaved form state, agreeing with the recognition indicator. Model configuration list remains unchanged after Test connection runs; no persistence side effects occurred.

## Pass/Fail Criteria

**Pass:**
- Each test result reflects the current unsaved field value (steps 5, 8).
- Recognition indicator agrees with each test result.
- Model list unchanged from baseline after Test connection runs (step 10).
- Reopening the model shows original saved values, not unsaved test values (step 11).

**Fail:**
- Any result reflects a stale value instead of current unsaved input.
- Recognition indicator disagrees with test result.
- Any model/credential was created, altered, or deleted as a result of Test connection.

## Notes

**Source functional tests:** ELITEA-4166 (evaluates unsaved form values), ELITEA-4167 (no persistence side effects)

**Regression rationale:** Consolidates two critical stateless behavior invariants: (1) Test connection must be a real-time preview reflecting current unsaved form state, not stale data; (2) Test connection must be read-only with zero persistence side effects. Regressions would cause high-impact data integrity issues (unintended saves) or confusing UX (stale results). Natural merged flow: modify form → test reflects unsaved values → navigate away → verify nothing saved.

**Selected checkpoints:**
- Test connection with unsaved valid Model Name → success result matches new value + recognition indicator agrees
- Test connection with unsaved invalid Model Name → failure result matches new value + recognition indicator agrees
- No model/credential created, altered, or deleted after Test connection runs
- Original saved values preserved after unsaved Test connection runs
