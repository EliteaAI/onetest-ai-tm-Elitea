---
id: ELITEA-1703
title: Verify newly created PGVector credential from Settings appears in toolkit dropdown
priority: critical
type: integration
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:settings, feat:toolkits, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has just created a new PGVector credential "test-pgvector-config" via Settings (see ELITEA-1702)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| New Credential Name | test-pgvector-config |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | After creating PGVector credential in Settings, navigate to Agents page | Agents page loads |
| 2 | Open any agent configuration OR create a new agent | Agent configuration page opens |
| 3 | Expand "Toolkit" section | Toolkit section expands |
| 4 | Click on "Pgvector Configuration" dropdown | Dropdown opens showing credentials list |
| 5 | Look for the newly created credential "test-pgvector-config" in the list | New credential "test-pgvector-config" appears in "SAVED PGVECTOR CREDENTIALS" list |
| 6 | Select the new credential | Credential is selected successfully |

## Expected Final State

Newly created PGVector credential is immediately available in the toolkit dropdown and can be selected.

## Pass/Fail Criteria

**Pass:**
- PGVector dropdown loads successfully
- Newly created credential "test-pgvector-config" appears in list
- New credential is available without page refresh (or after manual refresh)
- New credential can be selected
- Selection works correctly

**Fail:**
- New credential doesn't appear in dropdown
- Credential only appears after browser restart
- Credential appears but cannot be selected
- Dropdown doesn't load after credential creation
