---
id: ELITEA-0870
title: "Access Control — Trigger Config Editable Only by Users with Edit Permissions"
priority: medium
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [permissions, pipeline, security, R-2.0.3, trigger]
requirements: [#4827]
---
# ELITEA-0870: Access Control — Trigger Config Editable Only by Users with Edit Permissions

**Module:** Entrypoint Trigger Type · **Priority:** Medium · **Type:** Functional

**Objective:** Verifies that users with pipeline edit permissions can modify the trigger type and configuration, while users with read-only access can view but not modify trigger settings.

## Preconditions

Two user accounts are available in the same project:
  User A: has pipeline edit permissions
  User B: has read-only access to the pipeline
A pipeline with an Entrypoint node exists in the project

## Test Data

User A credentials (editor)
User B credentials (viewer/read-only)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User A (editor) and open the pipeline in edit mode | Pipeline opens in edit mode |
| 2 | Select the Entrypoint node and change the Trigger type (e.g., from Chat Message to Schedule) | The Trigger dropdown is interactive; type can be changed and configured |
| 3 | Save the change | Save is successful |
| 4 | Log out and log in as User B (read-only) | Logged in as User B |
| 5 | Navigate to the same pipeline | Pipeline is visible |
| 6 | Attempt to open the pipeline in edit mode or view the Entrypoint node config | The Trigger field and its configuration are visible/readable |
| 7 | Attempt to change the Trigger dropdown or modify the schedule/webhook config as User B | The Trigger dropdown and config fields are disabled or not accessible; changes cannot be made or saved |

## Expected Final State

The Trigger dropdown and config fields are disabled or not accessible; changes cannot be made or saved

## Pass/Fail Criteria

PASS: Editor can change trigger; read-only user sees config but cannot edit or save changes
FAIL: Read-only user can modify and save trigger changes; editor is blocked from editing
