---
id: ELITEA-4234
title: "Editor and Admin Roles: Save, Save As Version, and Discard Behavior Unchanged on Agent Details (Regression)"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#7302]
---

## Preconditions

- Two user accounts available: one with the **Editor** role and one with the **Admin** role, both with access to the same test Agent
- An existing Agent with no pending changes (Save disabled, Save As Version enabled per baseline, Discard disabled)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Roles | Editor, Admin |
| Agent | Any existing agent accessible to both roles |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as Editor. Open the test Agent's Details page with no pending changes. | Save is disabled, Save As Version is enabled, Discard is disabled — same baseline as before the fix. |
| 2 | Make a local edit (e.g. modify instructions text). | Save becomes enabled; Discard becomes enabled; Save As Version remains enabled. |
| 3 | Click Save. | Change persists successfully; no permission error is shown. |
| 4 | Make another local edit, then click Discard. | The local edit is reverted; Save and Discard return to disabled. |
| 5 | Click Save As Version. | A new version is created successfully. |
| 6 | Repeat steps 1–5 logged in as Admin. | Identical results — Save/Save As Version/Discard behave exactly as before the fix; no restriction is applied to Admin. |

## Expected Final State

Editor and Admin can fully use Save, Save As Version, and Discard on Agent Details with no behavior change introduced by the Viewer-targeted fix.

## Pass/Fail Criteria

**Pass:**
- Editor and Admin see identical Save/Save As Version/Discard behavior to pre-fix baseline
- All three actions succeed without any permission error for both roles

**Fail:**
- Editor or Admin experiences any new restriction, hidden control, disabled state, or permission error that did not exist before this fix
