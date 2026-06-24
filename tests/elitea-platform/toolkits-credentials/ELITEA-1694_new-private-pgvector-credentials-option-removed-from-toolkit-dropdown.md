---
id: ELITEA-1694
title: Verify "New private pgvector credentials" option is removed from toolkit PGVector Configuration dropdown
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:toolkits, nfr:ui, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1694: Verify "New private pgvector credentials" option is removed from toolkit PGVector Configuration dropdown

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "New private pgvector credentials" creation option has been removed from the toolkit-level PGVector Configuration dropdown as part of the UI simplification enhancement, ensuring users can only create credentials via Settings.

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to create/edit agents or toolkits
- At least one saved PGVector credential exists in the system

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Credential | elitea-pgvector |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents page | Agents page loads successfully |
| 2 | Click on an existing agent OR click "+ Create" to create a new agent | Agent configuration page opens |
| 3 | In the agent configuration, expand "Toolkit" section | Toolkit section expands showing configuration options |
| 4 | Locate "Pgvector Configuration" field | PGVector Configuration field is visible |
| 5 | Click on the PGVector Configuration dropdown to open it | Dropdown opens showing available options |
| 6 | Observe all available options in the dropdown | "New private pgvector credentials" option is NOT present; only "SAVED PGVECTOR CREDENTIALS" section with existing credentials is displayed |

## Expected Final State

PGVector Configuration dropdown displays only saved credentials without any "Create new" options for private credentials.

## Pass/Fail Criteria

**Pass:**
- "New private pgvector credentials" option is completely removed from toolkit dropdown
- Only "SAVED PGVECTOR CREDENTIALS" section is visible
- Existing saved credentials (e.g., "elitea-pgvector") are displayed correctly

**Fail:**
- "New private pgvector credentials" option still appears in dropdown
- Any "Create" option for private credentials is visible
- Dropdown layout or functionality is broken
