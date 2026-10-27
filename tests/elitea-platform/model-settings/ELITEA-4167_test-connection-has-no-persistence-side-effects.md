---
id: ELITEA-4167
title: "Test connection has no persistence side effects on the model or any other model/credential"
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
- Project has at least one existing LLM model configuration and one AI credential.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Scenario A | New LLM model form, valid values (success case) |
| Scenario B | New/existing form, invalid Model Name (failure case) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note current LLM model configuration list/values | Baseline recorded. |
| 2 | Run Scenario A (success case) via Test connection | Success result; no Save triggered. |
| 3 | Run Scenario B (failure case) via Test connection | Failure result; no Save triggered. |
| 4 | Without saving, navigate away or reload | Page navigates/reloads. |
| 5 | Review model/credential list | No new/altered model or credential as a result of either test. |

## Expected Final State

Model/credential list unchanged from baseline after both Test connection runs.

## Pass/Fail Criteria

**Pass:**
- No persisted changes from either test.

**Fail:**
- Any model/credential was created, altered, or deleted.
