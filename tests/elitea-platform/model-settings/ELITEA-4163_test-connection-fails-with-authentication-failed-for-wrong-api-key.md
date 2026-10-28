---
id: ELITEA-4163
title: "Test connection fails with Authentication failed for credential with wrong API key"
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
- A credential with a deliberately invalid/wrong API key exists or can be created.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Credential | Non-DIAL credential with invalid API key |
| Model Name | Valid model name for that provider |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select the credential with the invalid API key | Credential selected. |
| 2 | Enter a valid Model Name | Field accepts input. |
| 3 | Click Test connection | Result returned. |
| 4 | Observe result | "Authentication failed" with sanitized message. |
| 5 | Inspect message/network response | No API key, hostname/IP, or stack trace. |

## Expected Final State

Test connection reports "Authentication failed" with no sensitive data exposed.

## Pass/Fail Criteria

**Pass:**
- Category is "Authentication failed".
- No sensitive data in message/response.

**Fail:**
- Different category shown.
- Sensitive details exposed.
