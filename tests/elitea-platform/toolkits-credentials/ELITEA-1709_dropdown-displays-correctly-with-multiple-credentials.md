---
id: ELITEA-1709
title: Verify dropdown displays correctly with multiple saved PGVector credentials (2+)
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:toolkits, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least 3-5 PGVector credentials exist with different names
- User is on agent configuration page

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Credentials | elitea-pgvector, test-pgvector-1, test-pgvector-2, production-pgvector |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ensure multiple PGVector credentials exist (create if needed): elitea-pgvector, test-pgvector-1, test-pgvector-2, production-pgvector | At least 4 credentials exist |
| 2 | Navigate to agent configuration page | Page loads |
| 3 | Expand "Toolkit" section | Section expands |
| 4 | Click on "Pgvector Configuration" dropdown | Dropdown opens |
| 5 | Observe all displayed credentials | All saved credentials are displayed; each credential is displayed with correct name and icon; credentials are in consistent order |
| 6 | Check for scrollability if list is long | If many credentials exist (10+), dropdown is scrollable |

## Expected Final State

Dropdown correctly displays and handles multiple PGVector credentials with proper layout and scrollability.

## Pass/Fail Criteria

**Pass:**
- All saved credentials are displayed in dropdown
- Each credential is displayed with correct name and icon
- Credentials are in consistent order (alphabetical or by date)
- If many credentials exist, dropdown is scrollable
- No credentials are cut off or hidden
- Each credential item is individually clickable
- Hover effect works on each credential
- No visual overlap or layout issues

**Fail:**
- Some credentials are missing
- Credentials are displayed incorrectly
- No scrollability for long lists
- Layout is broken or overlapping
- Hover effects don't work
