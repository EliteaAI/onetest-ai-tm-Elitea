---
id: ELITEA-4169
title: "Test connection shows Rate limited result when the provider returns a rate-limit response"
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
- A credential/model combination that can be driven into a rate-limited state is available.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Credential/Model combination | Configured to trigger a provider rate-limit response |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure form with the rate-limit-triggering combination | Test connection enabled. |
| 2 | Click Test connection | Result returned. |
| 3 | Observe result category/message | "Rate limited" with sanitized message. |
| 4 | Inspect for sensitive details | None present. |

## Expected Final State

Rate-limit responses are categorized as "Rate limited" with a sanitized message.

## Pass/Fail Criteria

**Pass:**
- Category is "Rate limited"; no sensitive details present.

**Fail:**
- Different/generic category shown, or sensitive details exposed.
