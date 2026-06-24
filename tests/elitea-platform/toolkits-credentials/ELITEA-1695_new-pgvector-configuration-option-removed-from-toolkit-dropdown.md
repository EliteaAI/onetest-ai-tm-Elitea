---
id: ELITEA-1695
title: Verify "New pgvector configuration" option is removed from toolkit PGVector Configuration dropdown
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:toolkits, nfr:ui, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1695: Verify "New pgvector configuration" option is removed from toolkit PGVector Configuration dropdown

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "New pgvector configuration" creation option and any "CREATE" section have been completely removed from the toolkit PGVector Configuration dropdown, ensuring credential creation is only accessible via Settings.

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to create/edit agents or toolkits
- At least one saved PGVector credential exists in the system

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents page | Agents page loads successfully |
| 2 | Click on an existing agent OR click "+ Create" to create a new agent | Agent configuration page opens |
| 3 | In the agent configuration, expand "Toolkit" section | Toolkit section expands |
| 4 | Locate "Pgvector Configuration" field and click on the dropdown | Dropdown opens |
| 5 | Scroll through all available options in the dropdown | All options are visible |
| 6 | Check for "CREATE" section or "New pgvector configuration" option | Neither "CREATE" section nor "New pgvector configuration" option is present; only "SAVED PGVECTOR CREDENTIALS" section exists |

## Expected Final State

PGVector Configuration dropdown contains only the "SAVED PGVECTOR CREDENTIALS" section with no creation functionality visible.

## Pass/Fail Criteria

**Pass:**
- "New pgvector configuration" option is completely removed
- No "CREATE" section appears in the dropdown
- Only saved credentials section is displayed

**Fail:**
- "New pgvector configuration" option is still visible
- "CREATE" section exists in the dropdown
- Any creation functionality is accessible from toolkit dropdown
