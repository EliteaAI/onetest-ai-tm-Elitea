---
id: ELITEA-1699
title: Verify refresh icon appears to the right of "SAVED PGVECTOR CREDENTIALS" heading
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:toolkits, nfr:ui, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1699: Verify refresh icon appears to the right of "SAVED PGVECTOR CREDENTIALS" heading

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the refresh icon (circular arrow) appears on the right side of the "SAVED PGVECTOR CREDENTIALS" heading without any "Refresh" text label, matching the reference design.

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
| 5 | Locate the "SAVED PGVECTOR CREDENTIALS" heading | Heading is visible at top of dropdown |
| 6 | Observe the refresh icon position and styling | Refresh icon (circular arrow) appears on the right side of heading; icon is properly aligned vertically; no "Refresh" text label appears |
| 7 | Hover over the refresh icon | Cursor changes to pointer indicating clickability |

## Expected Final State

Refresh icon is positioned to the right of the "SAVED PGVECTOR CREDENTIALS" heading with no text label, matching the reference design.

## Pass/Fail Criteria

**Pass:**
- Refresh icon appears on the right side of heading
- Icon is properly aligned vertically with heading text
- Icon size is appropriate and matches other UI icons
- Icon is clickable (cursor changes to pointer on hover)
- NO "Refresh" text label appears - icon only
- Icon styling matches reference design

**Fail:**
- Refresh icon is missing or positioned incorrectly
- "Refresh" text label appears alongside icon
- Icon is not clickable or improperly styled
- Icon alignment is off
