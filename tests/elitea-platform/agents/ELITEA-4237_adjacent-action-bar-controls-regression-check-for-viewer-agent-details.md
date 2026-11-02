---
id: ELITEA-4237
title: "Adjacent Action-Bar Controls (Export, Three-Dot Menu) Unaffected for Viewer on Agent Details"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#7302]
---

## Preconditions

- A user account with the **Viewer** role, with access to an existing Agent
- Viewer is logged in and has the Agent Details page open

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Role | Viewer |
| Agent | Any existing agent accessible to the Viewer |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the Viewer-role user and open the test Agent's Details page. | Page loads normally. |
| 2 | Inspect the action bar for controls adjacent to Save/Save As Version/Discard, such as Export and the three-dot ("more actions") menu. | Each adjacent control retains its pre-fix visibility/enabled state for Viewer (e.g. if Export was previously visible/enabled for Viewer, it still is; it was not inadvertently hidden/disabled by this fix). |
| 3 | Click Export (if available to Viewer). | Export proceeds normally with no unexpected error introduced by this fix. |
| 4 | Open the three-dot menu (if present) and inspect its listed actions. | Only actions appropriate for Viewer are available in the menu (e.g. restricted actions remain hidden/disabled per pre-existing role rules, not newly affected by this fix); no previously-available read-only action has disappeared. |
| 5 | Confirm overall action-bar layout (spacing, alignment) is visually intact with Save/Save As Version/Discard now hidden. | No layout breakage (e.g. no overlapping elements, no leftover empty gap that looks broken) results from removing/disabling the three controls. |

## Expected Final State

All action-bar controls other than Save/Save As Version/Discard behave exactly as they did before this fix for the Viewer role, and the action bar remains visually intact.

## Pass/Fail Criteria

**Pass:**
- No adjacent control's visibility/enabled state changed as a side effect of this fix
- Action bar layout remains visually correct with the three controls hidden/disabled

**Fail:**
- Any adjacent control (Export, three-dot menu, or its entries) is unexpectedly hidden, disabled, or newly exposed for Viewer
- Visible layout regression (misalignment, overlap, broken spacing) in the action bar
