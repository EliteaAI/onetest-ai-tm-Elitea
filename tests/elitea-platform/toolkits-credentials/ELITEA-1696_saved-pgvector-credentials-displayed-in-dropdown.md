---
id: ELITEA-1696
title: Verify saved PGVector credentials are still displayed in the dropdown
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:toolkits, nfr:ui, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one PGVector credential exists (e.g., "elitea-pgvector")
- User has access to view/edit agents

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Expected Credential | elitea-pgvector |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents page | Agents page loads successfully |
| 2 | Open an existing agent OR create a new agent | Agent configuration page opens |
| 3 | Expand "Toolkit" section | Toolkit section expands |
| 4 | Click on "Pgvector Configuration" dropdown | Dropdown opens |
| 5 | Observe the displayed credentials list | "SAVED PGVECTOR CREDENTIALS" section heading is displayed; all existing saved PGVector credentials are listed with user icon next to each name |

## Expected Final State

All saved PGVector credentials are visible and accessible in the dropdown under the "SAVED PGVECTOR CREDENTIALS" section.

## Pass/Fail Criteria

**Pass:**
- "SAVED PGVECTOR CREDENTIALS" section heading is displayed
- All existing PGVector credentials are listed (e.g., "elitea-pgvector")
- Each credential name is clearly visible and readable
- User icon appears next to each credential

**Fail:**
- Saved credentials are missing or not displayed
- Section heading is missing or incorrect
- Credentials are not readable or properly formatted
- User icon is missing
