---
id: ELITEA-3208
title: "Share Toggle Is Disabled While the Secret Row Is Being Edited"
priority: medium
type: ui
module: secrets
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, ui]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3208: Share Toggle Disabled While Row Is Being Edited

**Module:** Secrets · **Priority:** Medium · **Type:** UI

**Objective:** Confirm the share toggle for a secret row is disabled (or otherwise prevented from being changed) while that same row is mid-edit, to avoid a race between an in-flight value edit and a share-state change.

**Coverage:** TC-UI (disabled while editing)

## Preconditions

- At least one secret exists and is not currently being edited

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click into edit mode for a secret's value (e.g. the edit/pencil icon). | Row enters edit mode. |
| 2 | Attempt to interact with that row's share toggle while still in edit mode. | Toggle is disabled/non-interactive, or a clear inline message explains it can't be changed mid-edit. |
| 3 | Cancel or save the edit, exiting edit mode. | Toggle becomes interactive again immediately. |
| 4 | Toggle it post-edit. | Change applies normally. |

## Expected Final State

The toggle cannot be changed while its row's value is mid-edit, and becomes available again as soon as editing ends.

## Pass/Fail Criteria

**Pass:**
- Toggle is disabled/blocked during edit mode and re-enabled immediately after

**Fail:**
- Toggle remains interactive during edit mode, allowing a race between value edit and share-state change
