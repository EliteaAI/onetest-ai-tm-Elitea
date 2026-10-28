---
id: ELITEA-4161
title: "Test connection succeeds for valid OpenAI or Azure OpenAI model and model recognition agrees"
priority: critical
type: functional
module: model-settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

## Preconditions

- User is logged in to `{{base_url}}` as a project admin.
- A saved non-DIAL AI credential (OpenAI or Azure OpenAI type) exists in the project.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Display Name | "QA Test Model" |
| Model Name (OpenAI) | A valid OpenAI model identifier, e.g. `gpt-4o-mini` |
| Model Name (Azure OpenAI) | A valid Azure OpenAI deployment identifier |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Settings → AI Providers → "+ AI Provider" → "LLM model" | New LLM Model Provider form opens. |
| 2 | Enter Display Name and a valid Model Name for OpenAI | Field accepts input. |
| 3 | Observe Model Name recognition indicator | Shows "Recognized: ..." for this valid identifier. |
| 4 | Select the saved OpenAI credential | Test connection becomes enabled. |
| 5 | Click Test connection without saving | Spinner shown; button not re-clickable during request. |
| 6 | Wait for completion | Result: "Connected in N s", consistent with step 3. |
| 7 | Repeat steps 2–6 for Azure OpenAI credential/model if available | Same success result, consistent with recognition indicator. |

## Expected Final State

Test connection reports success for both valid OpenAI and Azure OpenAI combinations, agreeing with the recognition indicator in each case. No model was saved.

## Pass/Fail Criteria

**Pass:**
- Both combinations show "Connected in N s".
- Recognition indicator agrees in both cases.

**Fail:**
- Any valid combination fails.
- Recognition indicator contradicts the result.
