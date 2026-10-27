---
id: ELITEA-4170
title: "Test connection shows Connection failed for network-level failures distinct from other categories"
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
- A credential pointing at a genuinely unreachable endpoint can be configured safely.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Credential | Configured with unreachable Api Base/endpoint |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure form with the unreachable-endpoint credential | Test connection enabled. |
| 2 | Click Test connection | Result returned. |
| 3 | Observe result | "Connection failed" with sanitized message. |
| 4 | Compare against the other failure categories | Not mistaken for Authentication failed, Model not found, or Rate limited. |

## Expected Final State

Connectivity-level failures are distinctly categorized as "Connection failed".

## Pass/Fail Criteria

**Pass:**
- Category is "Connection failed" and distinguishable from other categories.

**Fail:**
- Misclassified as a different category.
