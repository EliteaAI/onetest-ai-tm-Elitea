---
id: ELITEA-3209
title: "Platform-Managed/Default Secrets Cannot Be Toggled Shared/Private"
priority: high
type: ui
module: secrets
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, ui, default-secrets]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3209: Platform-Managed Secrets Cannot Be Toggled

**Module:** Secrets · **Priority:** High · **Type:** UI

**Objective:** Confirm platform-managed/default secrets do not expose an interactive share toggle (consistent with them being unreachable via `get_private_project_secret`, per ELITEA-3204) — the control is either absent or visibly disabled with an explanatory tooltip.

**Coverage:** TC-UI (platform-managed secrets can't be toggled)

## Preconditions

- A platform-managed/default secret is visible in the Secrets UI for the project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate a platform-managed/default secret row in the Secrets UI. | Row is visible. |
| 2 | Inspect its share toggle control. | Toggle is either absent, or present but disabled. |
| 3 | If disabled, hover over it. | Tooltip explains why it can't be toggled (e.g. "platform-managed secret"). |
| 4 | Attempt to force a toggle via direct interaction (click, keyboard). | No state change occurs; API is not called with a toggle request for this secret. |

## Expected Final State

Platform-managed secrets are visibly and functionally excluded from the share/private toggle.

## Pass/Fail Criteria

**Pass:**
- Toggle is absent or disabled for platform-managed secrets, with a clear explanation if disabled, and no toggle action is possible

**Fail:**
- Toggle is interactive on a platform-managed secret and a toggle action succeeds
