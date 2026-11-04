---
id: ELITEA-4344
title: "Verify Skills tab appears in Analytics after Agents & Pipelines tab when Skills module is enabled"
priority: critical
type: functional
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:skills, feat:analytics, r-2.0.8, nfr:usability]
requirements: [EliteaAI/elitea_issues#6929]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Skills module is enabled for the project
- User has permission to access Analytics

## Test Data

| Field | Value |
|-------|-------|
| Analytics URL | `{{base_url}}/settings/analytics` |
| Expected Tab Order | Overview, Costs, Tokens, Agents & Pipelines, **Skills**, Tools, Users, Activity, Health, Guide |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Analytics | Analytics page loads with default tab (Overview) |
| 2 | Observe the tab navigation bar at the top | Tab navigation bar displays all analytics tabs |
| 3 | Verify "Skills" tab is present in the tab list | "Skills" tab is visible |
| 4 | Verify "Skills" tab appears immediately after "Agents & Pipelines" tab | Tab order: ... Agents & Pipelines → **Skills** → Tools ... |
| 5 | Count the tab index position of "Skills" tab (0-indexed or 1-indexed) | Skills tab is at index 4 (after Overview=0, Costs=1, Tokens=2, Agents & Pipelines=3) |
| 6 | Click on "Skills" tab | Skills analytics page loads with Skill Activity table |
| 7 | Verify URL updates to include `?tab=skills` or similar query param | URL: `{{base_url}}/settings/analytics?tab=skills` |
| 8 | Navigate away to another tab (e.g., Costs) and then back to Skills | Skills tab loads correctly on return |
| 9 | Verify Skills tab is included in any interactive tour or tab-index-based guards | Interactive tour (if exists) accounts for Skills tab at correct position |
| 10 | Disable Skills module for the project (Admin → Modules or Settings) | Skills module disabled |
| 11 | Return to Settings → Analytics | Analytics page loads |
| 12 | Verify "Skills" tab is now hidden/not displayed | "Skills" tab not visible in tab list |

## Expected Final State

- Skills tab appears in Analytics after "Agents & Pipelines" when module is enabled
- Skills tab hidden when module is disabled
- Tab order is consistent and documented
- Interactive tour and guards updated for new tab position

## Pass/Fail Criteria

**Pass:**
- "Skills" tab present and visible when Skills module enabled
- Tab order: Agents & Pipelines → Skills → Tools
- URL updates correctly when Skills tab clicked
- Skills tab hidden when Skills module disabled
- No layout issues or broken tab navigation

**Fail:**
- "Skills" tab missing when Skills module enabled
- "Skills" tab appears in wrong position (not after Agents & Pipelines)
- URL does not update or incorrect query param
- "Skills" tab still visible when module disabled
- Interactive tour broken due to tab position change
