---
id: ELITEA-3469
title: "Artifact File Rename — Availability Follows Bucket-Level Permission, Falling Back to Default Project Role"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.7, comm:feedback]
requirements: [EliteaAI/elitea_issues#6438]
---

# ELITEA-3469: Artifact File Rename — Availability Follows Bucket-Level Permission, Falling Back to Default Project Role

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that artifact file rename visibility follows an explicit bucket-level permission override when set, and otherwise falls back to the user's default project role, across a private and a shared project.

---

## Preconditions

- A private project exists with an artifact bucket containing at least one file, owned by a user with full access.
- A shared/non-private project exists with an artifact bucket containing at least one file, and three test users are available covering the default project roles Admin, Editor, and Viewer.
- Ability to explicitly set a bucket-level permission override (read-only) for at least one of the shared-project users, independent of their project role.

## Test Data

| Scenario | Project type | Project role | Bucket-level override | Expected Rename availability (row menu + preview menu) |
|---|---|---|---|---|
| Owner | Private | Owner (full access) | N/A | Visible |
| Admin, default | Shared | Admin | None — default project role applies | Visible |
| Editor, default | Shared | Editor | None — default project role applies | Visible |
| Viewer, default | Shared | Viewer | None — default project role applies | Not visible |
| Editor, bucket read-only | Shared | Editor | Read-only | Not visible (overrides Editor role) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the private-project owner. Open the three-dot menu on a file row, then open the preview header three-dot menu. | "Rename" is visible in both locations. |
| 2 | Log in as the shared-project Admin user, no bucket-level override. Repeat step 1's checks. | "Rename" is visible in both locations. |
| 3 | Log in as the shared-project Editor user, no bucket-level override. Repeat step 1's checks. | "Rename" is visible in both locations. |
| 4 | Log in as the shared-project Viewer user, no bucket-level override. Repeat step 1's checks. | "Rename" is NOT visible in either location (default project permission denies Viewer). |
| 5 | Have the bucket-level permission for the Editor user explicitly set to read-only on the shared bucket. Log in as that Editor and repeat step 1's checks. | "Rename" is NOT visible in either location — the explicit bucket-level read-only permission overrides the Editor project role. If a rename is attempted through any other reachable path, it returns a permission-denied exception. |
| 6 | Across the Viewer and the read-only-overridden Editor scenarios above, confirm the bucket listing shows the original filenames unchanged. | No filename changes occurred for either denied scenario. |

## Expected Final State

Rename visibility/availability correctly reflects the bucket-level permission when one is explicitly set (read-only blocks rename even for an Editor), and otherwise falls back to the default project role (Admin and Editor visible, Viewer not visible), consistently across the row menu and preview menu, for both the private and shared project.

## Pass/Fail Criteria

**Pass:** Visibility matches the Test Data table for every scenario in both entry points; no filename changes occur for denied scenarios.
**Fail:** Rename is visible to the Viewer or to the read-only-overridden Editor, or missing for the Owner, Admin, or the default-permission Editor, in either entry point.
