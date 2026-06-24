---
id: ELITEA-1707
title: Verify checkmark appears next to currently selected PGVector credential
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:toolkits, nfr:ui, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least 2 saved PGVector credentials exist
- User is on agent configuration page

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Credential | elitea-pgvector |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to agent configuration page | Page loads |
| 2 | Expand "Toolkit" section | Section expands |
| 3 | Click on "Pgvector Configuration" dropdown | Dropdown opens |
| 4 | Select a credential (e.g., "elitea-pgvector") | Dropdown closes; selected credential displays in field |
| 5 | Reopen the PGVector Configuration dropdown | Dropdown opens |
| 6 | Observe the selected credential in the list | Checkmark (✓) icon appears next to "elitea-pgvector"; no other credentials have checkmarks |

## Expected Final State

Selected PGVector credential is clearly marked with a checkmark in the dropdown.

## Pass/Fail Criteria

**Pass:**
- Selected credential displays a checkmark (✓) icon
- Checkmark is clearly visible and positioned consistently
- Only ONE credential shows checkmark at a time
- Checkmark appears on the right side of credential name
- Checkmark color/style matches UI design system
- No checkmark appears for unselected credentials

**Fail:**
- Checkmark is missing for selected credential
- Multiple credentials show checkmarks
- Checkmark is positioned incorrectly
- Checkmark styling is inconsistent
