---
id: ELITEA-2492
title: "Empty State Display and Add Exception Flow"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts, nfr:ui]
requirements: [EliteaAI/elitea_issues#5912]
---

# ELITEA-2492: Empty State Display and Add Exception Flow

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify the empty state UI when no exceptions exist, and verify the complete flow of adding an exception via the empty state CTA button.

---

## Preconditions

- User (Admin) is logged in to the Elitea platform (Team project)
- A test bucket exists with NO permission exceptions (empty Exceptions list)
- At least one other user exists in the Team project

---

## Test Data

| Field | Value |
|-------|-------|
| Project | Team project |
| Bucket name | any name |
| User B | Test user to add as exception |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Login as Admin | Login successful |
| 2 | Navigate to Artifacts | Artifacts page loads |
| 3 | Select bucket with no exceptions | Bucket selected |
| 4 | Open Manage Permissions modal | Modal opens |
| 5 | Verify "Default Permissions" section | Shows "All users have read/write permissions by default." |
| 6 | Verify "Exceptions – 0" header | Count shows 0 |
| 7 | Verify empty state illustration is displayed | Illustration/icon visible |
| 8 | Verify empty state message | "No exceptions added yet" message displayed |
| 9 | Verify helper text | "All users have read/write permissions by default." |
| 10 | Verify "Add Exceptions" CTA button is present | Button visible and enabled |
| 11 | Click "Add Exceptions" button | Add exception modal opens |
| 12 | Select User B from Users dropdown | User B selected |
| 13 | Select "Read-only" permission | Permission selected |
| 14 | Click Save | Modal closes |
| 15 | Verify empty state is replaced with Exceptions table | Table now visible |
| 16 | Verify "Exceptions – 1" header | Count updated to 1 |
| 17 | Verify User B appears in table with "Read-only" | User B listed correctly |
| 18 | Verify table has columns: Checkbox, Name, Email, Permissions | All columns present |
| 19 | Edit User B to "Read & Write" to clean up | User B removed from table |
| 20 | Verify empty state returns | Empty state displayed again |

---

## Expected Final State

Empty state is displayed correctly when no exceptions exist. Adding an exception replaces empty state with table. Removing all exceptions restores empty state.

---

## Pass/Fail Criteria

**Pass:**
- Empty state shows all required elements (illustration, message, helper text, CTA)
- Adding exception via CTA works correctly
- Table replaces empty state after adding exception
- Removing all exceptions restores empty state

**Fail:**
- Empty state elements missing
- CTA button doesn't open Add modal
- Table doesn't appear after adding exception
- Empty state doesn't return after removing all exceptions
