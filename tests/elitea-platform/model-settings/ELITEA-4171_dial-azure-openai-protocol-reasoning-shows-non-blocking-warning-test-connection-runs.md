---
id: ELITEA-4171
title: "DIAL credential with Azure OpenAI protocol and Reasoning enabled shows non-blocking warning, Test connection still runs normally"
priority: high
type: functional
module: model-settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

## Preconditions

- User is logged in to `{{base_url}}` as a project admin.
- A saved DIAL credential exists in the project.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| DIAL Credential | Existing saved DIAL credential |
| API Protocol | Azure OpenAI |
| Supports Reasoning | Enabled, on a recognized GPT or Claude family model |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select the DIAL credential | API protocol field appears. |
| 2 | Set protocol to Azure OpenAI, enable Supports Reasoning for a GPT/Claude model | Both settings applied. |
| 3 | Observe Reasoning section | Non-blocking warning shown: "Reasoning may not work for this model with the Azure OpenAI protocol. Choose OpenAI or Anthropic for reasoning." Form remains usable; Save not blocked by this warning alone. |
| 4 | Enter a valid Model Name, click Test connection | A real request is sent (verify via network inspector). |
| 5 | Observe result | Result (success or a category failure) reflects the actual provider response — not short-circuited solely due to this protocol+reasoning combination. |

## Expected Final State

The Azure OpenAI + Reasoning combination shows only the existing non-blocking warning; Test connection still performs a real check.

## Pass/Fail Criteria

**Pass:**
- Non-blocking warning shown; Test connection sends a real request and returns a result based on the actual provider response.

**Fail:**
- Test connection is blocked/short-circuited solely due to this combination, or no warning is shown.
