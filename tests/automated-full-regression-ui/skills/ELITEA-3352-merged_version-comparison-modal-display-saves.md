---
id: ELITEA-3352
title: "Skill — Version Comparison (Modal, Display, Saves)"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, feat:version-comparison, feat:data-integrity, r-2.0.6, regression:merged, story:6304]
requirements: []
---

# ELITEA-3352: Skill — Version Comparison (Modal, Display, Saves)

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify complete version comparison functionality for skills including modal opening with side-by-side layout, correct version names in headers, instructions display, and independent save operations for each version. Success is confirmed when version comparison displays correctly, shows accurate data, and allows independent editing and saving of each version without affecting the other.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- User has permissions to create and edit skills and versions.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill Name | Version Comparison Test Skill |
| Base Version Description | Base version description for comparison testing |
| Base Version Instructions | Base version instructions: This is the original content for the base version. It includes baseline functionality. |
| Version 2 Name | Version 2 |
| Version 2 Description | Version 2 description with improvements |
| Version 2 Instructions | Version 2 instructions: This is the updated content for version 2. It includes enhanced functionality and improvements. |
| Version 1 Edit | Base version instructions: EDITED - This is the modified content for the base version. Changes applied to version 1 only. |
| Version 2 Edit | Version 2 instructions: EDITED - This is the further updated content for version 2. Additional changes applied to version 2 only. |

---

## Steps

### Part 1: Modal Opening with Side-by-Side Layout

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new skill with Name "Version Comparison Test Skill", Description "Base version description for comparison testing", Instructions "Base version instructions: This is the original content for the base version. It includes baseline functionality." | Skill is created successfully (base version) |
| 2 | Click "Save As Version" or "Create Version" button | Version creation dialog opens |
| 3 | Name the new version "Version 2" | Version name is entered |
| 4 | Update Description to "Version 2 description with improvements" | Description is updated |
| 5 | Update Instructions to "Version 2 instructions: This is the updated content for version 2. It includes enhanced functionality and improvements." | Instructions are updated |
| 6 | Save the new version | Version 2 is created successfully |
| 7 | Navigate to version comparison feature (e.g., click "Compare Versions" button, or select from version dropdown/menu) | Version comparison option is available |
| 8 | Select base version and Version 2 for comparison | Versions are selected |
| 9 | Click "Compare" or open the comparison modal | Comparison modal opens |
| 10 | Verify the modal displays side-by-side layout (two columns/panels) | Side-by-side layout is displayed |
| 11 | Verify left panel header shows "base" or the actual base version name | Left header shows correct version name |
| 12 | Verify right panel header shows "Version 2" or the actual version 2 name | Right header shows correct version name |
| 13 | Verify close button (X or "Close") is present and functional | Close control works correctly |

### Part 2: Instructions Display

| # | Action | Expected Result |
|---|--------|-----------------|
| 14 | In the comparison modal, verify the left panel (base version) displays instructions: "Base version instructions: This is the original content for the base version. It includes baseline functionality." | Base version instructions are displayed correctly |
| 15 | Verify the right panel (Version 2) displays instructions: "Version 2 instructions: This is the updated content for version 2. It includes enhanced functionality and improvements." | Version 2 instructions are displayed correctly |
| 16 | Verify both instructions are fully visible (no truncation or display errors) | Instructions are readable and complete |
| 17 | (If diff/highlighting is available) Verify differences between versions are highlighted or indicated | Differences are visually indicated |

### Part 3: Independent Saves — Edit and Save Version 1 (Base)

| # | Action | Expected Result |
|---|--------|-----------------|
| 18 | In the comparison modal, click "Edit" or enable editing for the left panel (base version) | Base version becomes editable |
| 19 | Modify the base version instructions to: "Base version instructions: EDITED - This is the modified content for the base version. Changes applied to version 1 only." | Instructions are edited |
| 20 | Click "Save" for the base version (left panel) | Base version is saved |
| 21 | Verify save success message or indicator appears | Save confirmation is shown |
| 22 | Verify the right panel (Version 2) instructions remain UNCHANGED: "Version 2 instructions: This is the updated content for version 2. It includes enhanced functionality and improvements." | Version 2 is not affected by base version save |
| 23 | Close the comparison modal | Modal closes |
| 24 | Re-open the comparison modal for base version and Version 2 | Comparison modal opens again |
| 25 | Verify base version instructions show the edited content: "Base version instructions: EDITED - This is the modified content for the base version. Changes applied to version 1 only." | Base version edits persisted |
| 26 | Verify Version 2 instructions remain unchanged: "Version 2 instructions: This is the updated content for version 2. It includes enhanced functionality and improvements." | Version 2 was not modified |

### Part 4: Independent Saves — Edit and Save Version 2

| # | Action | Expected Result |
|---|--------|-----------------|
| 27 | In the comparison modal, click "Edit" or enable editing for the right panel (Version 2) | Version 2 becomes editable |
| 28 | Modify Version 2 instructions to: "Version 2 instructions: EDITED - This is the further updated content for version 2. Additional changes applied to version 2 only." | Instructions are edited |
| 29 | Click "Save" for Version 2 (right panel) | Version 2 is saved |
| 30 | Verify save success message or indicator appears | Save confirmation is shown |
| 31 | Verify the left panel (base version) instructions remain UNCHANGED: "Base version instructions: EDITED - This is the modified content for the base version. Changes applied to version 1 only." | Base version is not affected by Version 2 save |
| 32 | Close the comparison modal | Modal closes |
| 33 | Re-open the comparison modal for base version and Version 2 | Comparison modal opens again |
| 34 | Verify base version instructions remain: "Base version instructions: EDITED - This is the modified content for the base version. Changes applied to version 1 only." | Base version unchanged by Version 2 edit |
| 35 | Verify Version 2 instructions show the edited content: "Version 2 instructions: EDITED - This is the further updated content for version 2. Additional changes applied to version 2 only." | Version 2 edits persisted |

### Part 5: Persistence After Close and Reopen

| # | Action | Expected Result |
|---|--------|-----------------|
| 36 | Close the comparison modal | Modal closes |
| 37 | Navigate away from the skill (e.g., go to Skills list) | Navigation completes |
| 38 | Re-open the skill "Version Comparison Test Skill" | Skill editor loads |
| 39 | Open the comparison modal again for base version and Version 2 | Comparison modal opens |
| 40 | Verify base version instructions show the last saved content: "Base version instructions: EDITED - This is the modified content for the base version. Changes applied to version 1 only." | Base version persisted correctly |
| 41 | Verify Version 2 instructions show the last saved content: "Version 2 instructions: EDITED - This is the further updated content for version 2. Additional changes applied to version 2 only." | Version 2 persisted correctly |
| 42 | Verify both versions maintained their independent edits (no cross-contamination) | Data integrity is maintained |

---

## Expected Final State

- Version comparison modal opens with side-by-side layout
- Correct version names are displayed in panel headers
- Instructions display correctly and completely for both versions
- Editing and saving Version 1 (base) does not affect Version 2
- Editing and saving Version 2 does not affect Version 1 (base)
- All edits persist correctly after close, navigation, and reopen
- Data integrity is maintained: no cross-contamination between versions

---

## Pass/Fail Criteria

**Pass:**
- Comparison modal opens with side-by-side layout
- Panel headers display correct version names ("base" and "Version 2")
- Instructions display correctly and completely in both panels
- Differences are highlighted or visually indicated (if feature available)
- Saving base version does not modify Version 2
- Saving Version 2 does not modify base version
- All edits persist after close and reopen
- No cross-contamination between versions

**Fail:**
- Modal does not open or layout is incorrect (not side-by-side)
- Version names in headers are incorrect or missing
- Instructions are truncated, missing, or displayed incorrectly
- Saving one version modifies the other version (cross-contamination)
- Edits do not persist after close and reopen
- Any step produces an error or unexpected result

---

## Notes

**Source functional tests:** ELITEA-3352, ELITEA-3353

**Regression rationale:** Consolidated from 2 tests covering version comparison feature: (1) ELITEA-3352 tests modal opening, side-by-side layout, correct version names in headers, and close controls, and (2) ELITEA-3353 tests instructions display correctness and independent save operations (saving one version doesn't affect the other). These tests cover different aspects of the same feature from UI structure to data integrity and can be naturally merged into a comprehensive version comparison test.

**Selected checkpoints:**
- Modal opens → side-by-side layout → correct version names in headers
- Instructions display correctly for both versions
- Edit base version → save → Version 2 unchanged
- Edit Version 2 → save → base version unchanged
- Close → reopen → both versions show their independent edits
- No cross-contamination between version saves
