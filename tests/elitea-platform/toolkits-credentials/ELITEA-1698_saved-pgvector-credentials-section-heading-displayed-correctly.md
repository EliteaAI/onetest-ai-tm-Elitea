---
id: ELITEA-1698
title: Verify "SAVED PGVECTOR CREDENTIALS" section heading is displayed correctly in dropdown
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
- At least one saved PGVector credential exists
- User has access to agent configuration

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents page | Agents page loads |
| 2 | Open any agent configuration | Agent configuration opens |
| 3 | Expand "Toolkit" section | Toolkit section expands |
| 4 | Click on "Pgvector Configuration" dropdown | Dropdown opens |
| 5 | Observe the section heading at the top of the dropdown | Section heading "SAVED PGVECTOR CREDENTIALS" is displayed in uppercase at the top of the dropdown, above the credentials list |

## Expected Final State

"SAVED PGVECTOR CREDENTIALS" heading is prominently displayed at the top of the dropdown with consistent styling matching the design system.

## Pass/Fail Criteria

**Pass:**
- Heading "SAVED PGVECTOR CREDENTIALS" is displayed in uppercase
- Heading uses same font style, size, and color as other section headings
- Heading is positioned at the top of the dropdown
- Heading is clearly distinguishable from credential items
- Styling matches reference design from issue screenshots

**Fail:**
- Heading is missing or incorrect
- Heading uses wrong casing or font
- Heading is positioned incorrectly
- Styling doesn't match design specifications
