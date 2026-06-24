---
id: ELITEA-1708
title: Verify dropdown displays correctly when no saved credentials exist (empty state)
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:toolkits, nfr:ui, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1708: Verify dropdown displays correctly when no saved credentials exist (empty state)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the PGVector Configuration dropdown handles the empty state gracefully when no credentials exist, showing appropriate messaging without errors.


## Preconditions

- User is logged in to `{{base_url}}`
- NO PGVector credentials exist in the system (delete all existing ones for this test)
- User is on agent configuration page

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ensure all PGVector credentials are deleted from Settings → AI Configuration | All credentials removed |
| 2 | Navigate to agent configuration page | Page loads |
| 3 | Expand "Toolkit" section | Section expands |
| 4 | Click on "Pgvector Configuration" dropdown | Dropdown opens |
| 5 | Observe the empty dropdown state | "SAVED PGVECTOR CREDENTIALS" heading appears; empty state message appears (e.g., "No credentials available") OR dropdown shows only heading with no items; refresh icon is present |

## Expected Final State

Dropdown gracefully handles empty state with appropriate messaging and no errors.

## Pass/Fail Criteria

**Pass:**
- Dropdown opens without errors
- "SAVED PGVECTOR CREDENTIALS" heading still appears
- Empty state message appears or dropdown shows only heading
- No JavaScript errors in console
- Refresh icon is present and functional
- User is guided to create credentials via Settings (optional helper text/link)

**Fail:**
- Dropdown fails to open or shows error
- Heading is missing
- No empty state handling
- JavaScript errors occur
- Dropdown appears broken
