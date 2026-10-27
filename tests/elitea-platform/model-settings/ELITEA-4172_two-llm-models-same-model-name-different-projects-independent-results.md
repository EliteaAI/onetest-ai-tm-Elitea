---
id: ELITEA-4172
title: "Two LLM models with the same Model Name in different projects produce independent Test connection results"
priority: high
type: functional
module: model-settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

## Preconditions

- User has access to two separate projects (A and B), each with its own AI credential.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Shared Model Name | `shared-model-name` (same in both projects) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Project A, set Model Name to "shared-model-name" with Project A's credential, run Test connection | Result noted. |
| 2 | In Project B, set the same Model Name with Project B's credential, run Test connection | Result reflects only Project B's combination. |
| 3 | Compare Project B's result to Project A's | Independent; unaffected by Project A's prior result. |

## Expected Final State

Results are correctly isolated per project despite identical Model Name values.

## Pass/Fail Criteria

**Pass:**
- Project B's result depends only on its own credential/model.

**Fail:**
- Project B's result is influenced by or identical to Project A's due to the shared name.
