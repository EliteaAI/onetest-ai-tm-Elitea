---
id: ELITEA-4375
title: "Save, Save As Version, and Discard Remain Hidden for Viewer on Pipeline Details (Regression)"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#7302]
---

## Preconditions

- A user account with the **Viewer** role in a project containing at least one existing Pipeline
- Pipeline Details page is accessible to the Viewer in read-only mode

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Role | Viewer |
| Pipeline | Any existing pipeline accessible to the Viewer |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the Viewer-role user. | Login succeeds. |
| 2 | Navigate to Pipelines and open an existing Pipeline's Details page. | Pipeline Details page loads in read-only mode. |
| 3 | Inspect Save, Save As Version, and Discard in the action bar/canvas toolbar. | All three remain hidden for the Viewer, consistent with pre-existing, correctly-implemented behavior referenced by this fix. |
| 4 | Attempt any local interaction with the canvas (e.g. selecting a node) that would normally surface pending-change state for an Editor. | None of the three controls appears for the Viewer. |
| 5 | Inspect the DOM for the three controls. | Elements are absent from the DOM — not CSS-hidden while still present. |

## Expected Final State

Pipeline Details continues to hide Save, Save As Version, and Discard for the Viewer role, unaffected by the Agent Details fix delivered under this issue.

## Pass/Fail Criteria

**Pass:**
- Save, Save As Version, and Discard remain hidden for Viewer on Pipeline Details
- No regression was introduced in Pipelines by the Agent Details fix

**Fail:**
- Any of the three controls becomes visible for Viewer on Pipeline Details
- Any control is only CSS-hidden while remaining present in the DOM
