---
id: ELITEA-4233
title: "Save, Save As Version, and Discard Remain Hidden or Disabled for Viewer on Skill Details (Regression)"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#7302]
---

## Preconditions

- A user account with the **Viewer** role in a project containing at least one existing Skill
- Skill Details page is accessible to the Viewer in read-only mode

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Role | Viewer |
| Skill | Any existing skill accessible to the Viewer |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the Viewer-role user. | Login succeeds. |
| 2 | Navigate to Skills and open an existing Skill's Details page. | Skill Details page loads in read-only mode. |
| 3 | Inspect Save, Save As Version, and Discard controls. | All three remain hidden or disabled for the Viewer, consistent with the pre-existing, correctly-implemented behavior referenced by this fix (see ELITEA-3340 for the related Compare Versions permission check). | 
| 4 | Attempt to trigger Compare Versions / any action that surfaces version-editing affordances. | Save/Save As Version/Discard remain hidden or disabled; a clear permission error is shown if any restricted action is bypassed. |
| 5 | Inspect the DOM for the three controls. | Elements are absent or present with a disabled state — not CSS-hidden while still interactive. |

## Expected Final State

Skill Details continues to hide/disable Save, Save As Version, and Discard for the Viewer role, unaffected by the Agent Details fix delivered under this issue.

## Pass/Fail Criteria

**Pass:**
- Save, Save As Version, and Discard remain hidden or disabled for Viewer on Skill Details
- No regression was introduced in Skills by the Agent Details fix

**Fail:**
- Any of the three controls becomes visible/clickable for Viewer on Skill Details
- Any control is only CSS-hidden while remaining present and enabled in the DOM
