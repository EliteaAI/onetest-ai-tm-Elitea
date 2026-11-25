---
id: ELITEA-4517
title: "Verify a Tavily credential can be created with only the API Key field and Test Connection reflects validity"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- User is logged in to `{{base_url}}` with access to create credentials in a project

## Test Data

| Field | Value |
|-------|-------|
| Credential type | Tavily |
| Valid API key | A valid Tavily API key |
| Invalid API key | A deliberately invalid/garbage value |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Go to Credentials → Create new credential → select type "Tavily" | Form shows exactly: Display Name, ID, and "Api Key" (masked, with Secret/Password view toggle) — no other fields |
| 2 | Enter a valid API key, save, click "Test connection" | A clear success message/indicator is shown |
| 3 | Create a second credential with a deliberately invalid API key, click "Test connection" | A clear failure message is shown — no raw error or stack trace |
| 4 | Toggle the Secret/Password view on the saved key and inspect page source | The API key value is never exposed in plain text anywhere in the UI after saving |

## Expected Final State

A Tavily credential with only the Api Key field exists, and Test Connection correctly distinguishes valid from invalid keys.

## Pass/Fail Criteria

**Pass:**
- Form shows only the documented field
- Test Connection succeeds for a valid key and fails cleanly for an invalid key
- The key is never exposed in plain text

**Fail:**
- An extra field (e.g. base URL) is present
- Test Connection misreports validity
- The key is exposed anywhere in the UI
