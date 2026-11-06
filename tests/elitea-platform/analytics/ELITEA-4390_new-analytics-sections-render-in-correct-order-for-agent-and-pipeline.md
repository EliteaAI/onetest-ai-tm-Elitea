---
id: ELITEA-4390
title: "New Versions, Models, Trigger Sources, and Recent Runs sections render in correct order for Agent and Pipeline detail views"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, layout]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4390: New Versions, Models, Trigger Sources, and Recent Runs sections render in correct order for Agent and Pipeline detail views

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Agent and Pipeline Analytics detail view renders the four new sections (Versions, Models, Trigger Sources, Recent Runs) alongside the existing sections, in the exact required order, without disturbing existing content.

**Coverage:**
- Required content order: KPI cards → Runs by Day → Versions/Models (two-column) → Users/Tools → Trigger Sources → Recent Runs
- Existing KPI cards, Runs by Day chart, Users table, and Tools table remain present and unaffected
- Order holds for both an Agent and a Pipeline detail view

## Preconditions

- Logged in to `{{base_url}}`
- At least one Agent and one Pipeline exist in the project with run history
- Confirmed build/version deployed to the test environment includes EL-7033

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity 1 | Agent with run history |
| Entity 2 | Pipeline with run history |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Analytics → Agents & Pipelines, select an Agent with run history | Detail view opens |
| 2 | Scroll top to bottom and record the order of sections rendered | Order is: existing KPI cards, existing Runs by Day chart, Versions and Models (side by side), existing Users and Tools, Trigger Sources, Recent Runs |
| 3 | Confirm the existing KPI cards, Runs by Day chart, Users table, and Tools table are all still present and show the same data style/format as before | No existing section is missing, hidden, or visually altered |
| 4 | Repeat steps 1–3 for a Pipeline with run history | Same section order and existing-content preservation confirmed for the Pipeline detail view |

## Expected Final State

Both Agent and Pipeline detail views display all existing sections plus the four new sections in the exact specified order, with no regression to previously existing content.

## Pass/Fail Criteria

**Pass:**
- Section order matches the specification exactly for both Agent and Pipeline
- All pre-existing sections (KPI cards, Runs by Day, Users, Tools) remain present and unmodified

**Fail:**
- Any new section is missing, duplicated, or out of order
- Any pre-existing section is missing, hidden, or altered
- Order differs between Agent and Pipeline detail views
