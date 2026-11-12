---
id: ELITEA-4563
title: "Toolkit-test and secret-masking flows remain correct for non-Web-Search toolkits"
priority: medium
type: regression
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- At least one non-Web-Search toolkit with valid credentials (e.g. GitHub, Jira) available for testing
- A remote MCP toolkit available with its "test settings panel" accessible
- Access to the Secrets settings page and a sensitive-tool-calling authorization dialog

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/toolkits` |
| Related existing cases | ELITEA-0991, ELITEA-0992, ELITEA-1005, ELITEA-2928, ELITEA-1933, ELITEA-1935, ELITEA-1937 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run "Test"/"Test connection" on a non-Web-Search toolkit with valid credentials | Success is reported correctly in the UI; any underlying socket payload has credentials masked |
| 2 | Run the same test action with intentionally invalid credentials | Failure message remains informative to the user; underlying event remains free of secret values |
| 3 | Open the Secrets settings page and verify the unmask/copy behavior for an existing secret | Behaves as before (ELITEA-0991/0992), unaffected by the masking change |
| 4 | Trigger a sensitive-tool-calling authorization dialog and verify sensitive parameter masking | Behaves as before (ELITEA-1005/2928) |
| 5 | Open a remote MCP toolkit's "test settings panel," load tools, and run a selected tool | Tools load and execute correctly (ELITEA-1933/1935/1937 behavior unaffected) |

## Expected Final State

All existing toolkit-test and secret-masking flows unrelated to Web Search continue to function correctly after the socket-masking hardening fix.

## Pass/Fail Criteria

**Pass:**
- All re-checked flows behave as previously verified, with credentials masked and no functional regression

**Fail:**
- Any non-Web-Search toolkit test, secret-masking display, or MCP test-settings flow breaks or stops masking correctly
