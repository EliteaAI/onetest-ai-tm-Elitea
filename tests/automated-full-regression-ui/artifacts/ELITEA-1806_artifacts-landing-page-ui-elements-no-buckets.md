---
id: ELITEA-1806
title: "Artifacts Landing Page – UI Elements with No Buckets"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1806: Artifacts Landing Page – UI Elements with No Buckets

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Artifacts landing page renders the correct empty state UI when a project has no buckets created, including the "No buckets created yet" message in both panels and a zero-count footer.

---

## Preconditions

- User is logged in to the Elitea platform.
- The project has no buckets created.

---

## Test Data

| Field | Value |
|-------|-------|
| Buckets count | 0 |
| Size | 0 B |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts page in a project that has no buckets created | Artifacts page loads |
| 2 | Verify the left panel header displays "BUCKETS" label with a folder (create bucket) icon and a search (magnifier) icon | Header is correctly displayed with both icons |
| 3 | Verify the left panel body shows the text "No buckets created yet" and subtitle "Create your first bucket to get started" | Both messages are shown in the left panel |
| 4 | Verify the main (right) content area displays a placeholder icon centered on the page | Placeholder icon is visible in the center |
| 5 | Verify the text "No buckets created yet" is displayed below the placeholder icon in the main area | Message is displayed below the icon |
| 6 | Verify the bottom of the left panel shows "Buckets: 0  Size: 0 B" | Footer shows 0 buckets and 0 B size |

---

## Expected Final State

The Artifacts page for a project with no buckets shows the correct empty state in both panels: "No buckets created yet" message with subtitle in the left panel, a centered placeholder in the main area, and a zero-count footer.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Both empty state messages, placeholder icon, and zero-count footer are displayed correctly.

**Fail:**
- Any step produces an error or unexpected result.
- Empty state messages or placeholder are missing, or footer shows incorrect values.
