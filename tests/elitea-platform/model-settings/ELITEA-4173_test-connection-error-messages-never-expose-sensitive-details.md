---
id: ELITEA-4173
title: "Test connection error messages never expose API keys, hostnames, IP addresses, or stack traces across all failure categories"
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
- Able to trigger Authentication failed, Model not found, Wrong API protocol or route, Rate limited, and Connection failed, per their dedicated scenarios.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Failure categories | Authentication failed, Model not found, Wrong API protocol or route, Rate limited, Connection failed |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1-5 | Trigger each of the five failure categories in turn via Test connection | Failure message shown for each. |
| 6 | For each, inspect the on-screen message and raw network response | None contain an API key, internal hostname/IP, or stack trace. |

## Expected Final State

All tested failure categories display sanitized messages with no sensitive internal details exposed.

## Pass/Fail Criteria

**Pass:**
- No category exposes sensitive details.

**Fail:**
- Any category exposes an API key, hostname/IP, or stack trace.
