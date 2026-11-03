---
id: ELITEA-4374
title: "Save, Save As Version, and Discard Are Hidden for Viewer on Agent Details"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#7302]
---

## Preconditions

- A user account with the **Viewer** role in a project containing at least one existing Agent (e.g. `Special Testing` project)
- Agent Details page is accessible to the Viewer in read-only mode

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Role | Viewer |
| Project | `Special Testing` |
| Agent | Any existing agent, e.g. `Confluence Cloud Toolkit` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the Viewer-role user. | Login succeeds. |
| 2 | Navigate to Agents and open the test Agent's Details page. | Agent Details page loads in read-only mode. |
| 3 | Inspect the Save, Save As Version, and Discard controls in the action bar. | All three are hidden — absent from the DOM, not merely visually suppressed via CSS while remaining present in the DOM. |
| 4 | Attempt to make a local edit normally available to the Viewer (e.g. type into an editable-looking field, if any field accepts input) that would enable Save for an Editor. | Save, Save As Version, and Discard remain hidden; no local edit causes them to appear or become active for the Viewer. |
| 5 | Inspect the DOM (via browser dev tools Elements panel) for the three controls. | Elements are absent from the DOM — not just CSS-hidden while still present. |

## Expected Final State

The Agent Details action bar shows no interactive Save, Save As Version, or Discard control for the Viewer role, regardless of any local, non-persisted edits made during the session.

## Pass/Fail Criteria

**Pass:**
- Save, Save As Version, and Discard are hidden for the Viewer at all times on Agent Details
- No local edit causes any of the three controls to appear

**Fail:**
- Any of the three controls is visible for the Viewer
- A control is only CSS-hidden while remaining present in the DOM
- A local edit causes any of the three controls to appear for the Viewer
