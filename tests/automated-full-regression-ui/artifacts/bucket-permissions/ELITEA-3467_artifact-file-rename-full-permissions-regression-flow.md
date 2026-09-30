---
id: ELITEA-3467
title: "Rename Artifact File — Full Permissions Regression Flow"
priority: high
type: regression
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.7, comm:feedback, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#6438]
---

# ELITEA-3467: Rename Artifact File — Full Permissions Regression Flow

**Module:** artifacts · **Priority:** high · **Type:** regression

**Objective:** Verify that artifact file rename availability correctly follows an explicit bucket-level permission override when set, and otherwise falls back to the user's default project role, consistently across the row menu and preview menu.

---

## Preconditions

- A test bucket with at least one file, accessible to users covering three **default project roles**: Admin, Editor, Viewer.
- Ability to explicitly set a **bucket-level permission override** (read-only) for at least one of those users, independent of their project role. Rename availability is governed first by any explicit bucket-level permission; only when no bucket-level permission is set does the user's default project role apply (Admin and Editor can rename; Viewer cannot).

## Test Data

| Scenario | Project role | Bucket-level permission override | Expected: Rename available (row menu + preview menu) |
|---|---|---|---|
| Admin, default | Admin | None — falls back to default project role | Yes |
| Editor, default | Editor | None — falls back to default project role | Yes |
| Viewer, default | Viewer | None — falls back to default project role | No |
| Admin, bucket set to read-only | Admin | Read-only | No (blocked despite Admin role) |
| Editor, bucket set to read-only | Editor | Read-only | No (blocked despite Editor role) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as a user with default project role Admin, no bucket-level override on the test bucket. Open the three-dot menu on a file row. | "Rename" is visible. |
| 2 | As the same user, open a file preview and check the preview header three-dot menu. | "Rename" is visible. |
| 3 | Log in as a user with default project role Editor, no bucket-level override. Repeat steps 1–2. | "Rename" is visible in both locations. |
| 4 | Log in as a user with default project role Viewer, no bucket-level override. Repeat steps 1–2. | "Rename" is NOT visible in either the row menu or preview menu (default project permission denies Viewer). |
| 5 | Have the bucket-level permission for the Admin or Editor user explicitly set to read-only on the test bucket. Log in as that user and repeat steps 1–2. | "Rename" is NOT visible in either location — the explicit bucket-level read-only permission overrides the Admin/Editor project role. |
| 6 | With the same read-only-overridden user, attempt to trigger a rename via any reachable path (e.g. a direct action if the UI exposes one). | The attempt returns a permission-denied exception; no filename change occurs. |
| 7 | Across all scenarios above, confirm the bucket listing shows the original filenames unchanged. | No filename changes occurred for any role/override combination. |

## Expected Final State

Rename availability correctly follows the bucket-level permission when one is explicitly set (read-only blocks rename regardless of project role), and otherwise falls back to the default project role: Admin and Editor can rename, Viewer cannot. This holds consistently across both the row menu and the preview menu.

## Pass/Fail Criteria

**Pass:**
- Availability matches the Test Data table for every scenario, in both the row menu and the preview menu.
- No filename changes occur for any denied role/override during the flow.

**Fail:**
- Rename is available for Viewer with no bucket override, or for Admin/Editor when the bucket is explicitly set to read-only.
- Rename is hidden for Admin or Editor when no bucket-level override exists.
