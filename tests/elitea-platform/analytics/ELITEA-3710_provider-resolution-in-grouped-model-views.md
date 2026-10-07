---
id: ELITEA-3710
title: "Verify Cost/Usage by Model Resolves the Correct Provider After a Model's Provider Configuration Changes"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6574]
---

# ELITEA-3710: Verify Cost/Usage by Model Resolves the Correct Provider After a Model's Provider Configuration Changes

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify "Cost by Model"/"Usage by Model" resolves the correct underlying provider per model, including after a model's provider configuration changes.

**Coverage:**
- Per-model cost/usage rows remain accurate across a provider-config change for the same model name

## Preconditions

- Admin access to AI Providers and Analytics "Cost by Model" / Usage "Usage by Model"
- A model whose underlying provider configuration (credentials/endpoint) can be changed without renaming the model

## Test Data

| Field | Value |
|-------|-------|
| Model name | Backed initially by Provider Configuration A |
| New config | Provider Configuration B, same model name |
| Message | "Hello" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note the provider backing the test model name in AI Providers configuration (Provider A) | Recorded |
| 2 | Send the test message against the model | Response received; usage recorded against Provider A |
| 3 | In AI Providers, change the model's underlying provider configuration to Provider B (same model name, different credentials/endpoint) | Configuration updated successfully |
| 4 | Send the test message again against the same model name | Response received; usage recorded against Provider B |
| 5 | Open Analytics > Costs ("Cost by Model") and Usage ("Usage by Model") for a window spanning both calls | Both calls appear under the model name without their provider attribution being silently merged, dropped, or misreported across the configuration change |

## Expected Final State

Per-model cost/usage rows remain accurate across a provider-configuration change for the same model name, for both the historical and new data.

## Pass/Fail Criteria

**Pass:**
- Both calls' usage correctly reflects their respective time periods without provider-attribution errors

**Fail:**
- Usage from either period is lost, merged incorrectly, or misattributed after the configuration change
