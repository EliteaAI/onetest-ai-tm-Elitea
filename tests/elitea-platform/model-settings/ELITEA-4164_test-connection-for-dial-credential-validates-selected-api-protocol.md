---
id: ELITEA-4164
title: "Test connection for DIAL credential validates selected API protocol against the model"
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
- A saved DIAL credential exists, with a known model name and its correct API protocol.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| DIAL Credential | Existing saved DIAL credential |
| Model Name | Known valid DIAL deployment/model name |
| Protocols | Correct protocol for the model, and an incorrect one |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select the DIAL credential | API protocol field appears. |
| 2 | Enter the known valid Model Name | Field accepts input. |
| 3 | Select the wrong protocol, click Test connection | Failure result (e.g. "Wrong API protocol or route"). |
| 4 | Change to correct protocol, click Test connection again | Success result ("Connected in N s"). |

## Expected Final State

Test connection distinguishes wrong vs. correct protocol for the same DIAL model/credential.

## Pass/Fail Criteria

**Pass:**
- Wrong protocol fails, correct protocol succeeds, for the same model/credential.

**Fail:**
- Either protocol produces the opposite result.
