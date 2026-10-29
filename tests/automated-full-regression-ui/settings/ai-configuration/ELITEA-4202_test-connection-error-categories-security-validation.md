---
id: ELITEA-4202
title: "Test connection error categories and security - Model not found, Authentication failed, Rate limited, Connection failed, no sensitive exposure"
priority: critical
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

## Preconditions

- User is logged in to `{{base_url}}` as a project admin.
- Project has:
  - A credential with deliberately invalid/wrong API key
  - A credential with valid API key
  - A credential pointing at an unreachable endpoint
  - A credential/model combination that can trigger rate-limit response

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Invalid Model Name | A misspelled/non-existent model id (e.g., `gpt-5.6wrongmodel`) |
| Wrong API Key Credential | Non-DIAL credential with invalid API key |
| Unreachable Endpoint Credential | Credential with genuinely unreachable Api Base |
| Rate-limit-triggering Combination | Credential/model configured to trigger provider rate-limit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Category 1: Model not found** |
| 1 | Open LLM model form, select a valid credential, enter an invalid Model Name | Field accepts input. |
| 2 | Observe recognition indicator | Shows "Not recognized..." |
| 3 | Click Test connection | Result returned. |
| 4 | Observe result category and message | "Model not found" with sanitized message. |
| 5 | Inspect message and network response | **Security check**: No API key, hostname/IP, or stack trace. |
| 6 | Compare recognition indicator (step 2) vs. result (step 4) | Both agree the name is invalid. |
| **Category 2: Authentication failed** |
| 7 | Clear form, select the wrong-API-key credential, enter valid Model Name | Credential selected. |
| 8 | Click Test connection | Result returned. |
| 9 | Observe result category and message | "Authentication failed" with sanitized message. |
| 10 | Inspect message and network response | **Security check**: No API key, hostname/IP, or stack trace. |
| **Category 3: Rate limited** |
| 11 | Clear form, configure rate-limit-triggering combination | Test connection enabled. |
| 12 | Click Test connection | Result returned. |
| 13 | Observe result category and message | "Rate limited" with sanitized message. |
| 14 | Inspect message and network response | **Security check**: No API key, hostname/IP, or stack trace. |
| **Category 4: Connection failed** |
| 15 | Clear form, select unreachable-endpoint credential, enter valid Model Name | Test connection enabled. |
| 16 | Click Test connection | Result returned. |
| 17 | Observe result category and message | "Connection failed" with sanitized message. |
| 18 | Compare against other categories | Distinctly categorized, not mistaken for Authentication/Model not found/Rate limited. |
| 19 | Inspect message and network response | **Security check**: No API key, hostname/IP, or stack trace. |

## Expected Final State

All four error categories are correctly identified with sanitized messages. Security validation confirms no sensitive data (API keys, hostnames/IPs, stack traces) is exposed in any failure category.

## Pass/Fail Criteria

**Pass:**
- All four categories show correct classification and sanitized messages.
- Recognition indicator agrees with Model not found result.
- **All categories pass security check**: no API key, hostname/IP, or stack trace in any message or network response.

**Fail:**
- Any category is misclassified or shows different/generic category.
- Any category exposes sensitive details.

## Notes

**Source functional tests:** ELITEA-4162 (Model not found), ELITEA-4163 (Authentication failed), ELITEA-4169 (Rate limited), ELITEA-4170 (Connection failed), ELITEA-4173 (Security - no sensitive data exposure)

**Regression rationale:** Consolidates all error-handling paths into one comprehensive journey. Security validation (no sensitive data leakage) must be verified across ALL error categories, not just one. High-impact if error categorization breaks (user confusion, incorrect troubleshooting) or sensitive data leaks (security incident). This merged test protects multiple distinct failure modes efficiently.

**Selected checkpoints:**
- Model not found: wrong model name → correct category + recognition indicator agrees + no sensitive data
- Authentication failed: wrong API key → correct category + no sensitive data
- Rate limited: rate-limit response → correct category + no sensitive data
- Connection failed: unreachable endpoint → correct category distinct from other categories + no sensitive data
