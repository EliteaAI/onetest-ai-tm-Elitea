---
id: ELITEA-4201
title: "Test connection succeeds for valid OpenAI and Azure OpenAI models, model recognition agrees"
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
- A saved non-DIAL OpenAI credential exists in the project.
- A saved non-DIAL Azure OpenAI credential exists in the project.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Display Name | "Regression Test Model" |
| OpenAI Model Name | A valid OpenAI model identifier, e.g. `gpt-4o-mini` |
| Azure OpenAI Model Name | A valid Azure OpenAI deployment identifier |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Settings → AI Providers → "+ AI Provider" → "LLM model" | New LLM Model Provider form opens. |
| 2 | Enter Display Name and a valid OpenAI Model Name | Field accepts input. |
| 3 | Observe Model Name recognition indicator | Shows "Recognized: ..." for this valid identifier. |
| 4 | Select the saved OpenAI credential | Test connection becomes enabled. |
| 5 | Click Test connection without saving | Spinner shown; button not re-clickable during request. |
| 6 | Wait for completion | Result: "Connected in N s", consistent with recognition indicator (step 3). |
| 7 | Clear the form, repeat steps 2–6 for Azure OpenAI credential and valid Azure deployment name | Same success result, consistent with recognition indicator. |

## Expected Final State

Test connection reports success for both valid OpenAI and Azure OpenAI combinations, agreeing with the recognition indicator in each case. No model was saved.

## Pass/Fail Criteria

**Pass:**
- Both combinations show "Connected in N s".
- Recognition indicator agrees with test result in both cases.

**Fail:**
- Any valid combination fails.
- Recognition indicator contradicts the result.

## Notes

**Source functional tests:** ELITEA-4161

**Regression rationale:** Critical smoke test for the core Test connection functionality. Validates both major non-DIAL provider types (OpenAI and Azure OpenAI) and ensures model recognition indicator consistency. Essential baseline for all model configuration workflows.

**Selected checkpoints:**
- Valid OpenAI credential + model → success
- Valid Azure OpenAI credential + deployment → success
- Recognition indicator agrees with test result for both providers
