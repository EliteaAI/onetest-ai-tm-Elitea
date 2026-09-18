---
id: ELITEA-3387
title: "Manage Permissions Modal: Empty State"
priority: medium
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3387: Manage Permissions Modal — Empty State

**Module:** Social Folders · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the content and behavior of the Manage Permissions modal when a folder has zero exceptions.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Logged in as Admin on a Team project
- Target folder has zero exceptions

## Test Data
- URL: {{base_url}}/app/
- Folder: any in-scope folder with 0 exceptions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Hover the folder, open the 3-dot menu, click **Manage permissions** | Modal titled **Manage Permissions: <folder name>** opens |
| 2 | Inspect the modal content | Shows: **Default Permissions** heading, the standard copy ("By default, users retain the permissions granted by their project roles. Exceptions can only restrict access."), **Exceptions – 0**, empty-state illustration, "No exceptions added yet", "Users retain the permissions granted by their project roles.", and a **+ add exception** action |
| 3 | Click the **X** icon | Modal closes |

## Expected Final State
No exceptions created; modal closed.

## Pass/Fail Criteria
**Pass:**
- All listed copy/elements are present exactly as described
- The modal closes via the X icon

**Fail:**
- Any listed element is missing or mislabeled
- The modal fails to close
