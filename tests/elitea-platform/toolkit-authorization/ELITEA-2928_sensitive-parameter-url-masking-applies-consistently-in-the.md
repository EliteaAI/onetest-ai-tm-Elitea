---
id: ELITEA-2928
title: "Sensitive parameter/URL masking applies consistently in the toolkit-authorization popup's Authorization details"
priority: high
type: functional
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An OAuth-requiring toolkit (no valid token), whose credential configuration could surface a sensitive value (e.g. client identifier), is addable to a chat

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Reference pattern | Sensitive Action dialog parameter masking |
| Under test | Toolkit Authorization Required popup's Authorization details |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger the popup for a toolkit whose Authorization details could include a sensitive value | Popup appears with an "Authorization details" section |
| 2 | Expand "Authorization details" | Section expands to show Toolkit server / Resource metadata / Authorization server / Scopes |
| 3 | Inspect all displayed values for secrets/tokens | Only non-secret values (server URLs, scopes) are shown; any secret/token-like value is masked using the same masking rules as the Sensitive Action dialog |

## Expected Final State

The Authorization details section never exposes raw secret or token values; masking, where applicable, is consistent with the existing Sensitive Action dialog's parameter masking behavior.

## Pass/Fail Criteria

**Pass:**
- No raw secret/token values are visible in Authorization details
- Any masked value follows the same masking convention as the Sensitive Action dialog

**Fail:**
- A raw secret or token value is exposed unmasked in Authorization details
- Masking format is inconsistent with the Sensitive Action dialog's established convention
