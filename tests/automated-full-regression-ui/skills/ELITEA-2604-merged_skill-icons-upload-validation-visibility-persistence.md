---
id: ELITEA-2604
title: "Skill — Icons (Upload, Validation, Visibility, Persistence)"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, feat:icon, feat:versioning, regression:merged]
requirements: []
---

# ELITEA-2604: Skill — Icons (Upload, Validation, Visibility, Persistence)

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify complete icon management lifecycle for skills including uploading custom icons with format validation, file size enforcement, deletion (revert to default), visibility across all UI locations, and persistence across versions. Success is confirmed when all icon operations work correctly and icons display consistently throughout the UI.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- Test image files are available:
  - Valid PNG file under 500KB
  - Valid JPG file under 500KB
  - Valid GIF file under 500KB (optional)
  - Valid WEBP file under 500KB (optional)
  - Invalid file over 500KB (e.g., 600KB PNG)
  - Invalid file type (e.g., .txt, .pdf, .svg)

---

## Test Data

| Field | Value |
|-------|-------|
| Skill Name | Icon Test Skill |
| Skill Description | Skill for testing icon functionality |
| Skill Instructions | Test instructions for icon skill |
| Valid icon file | icon-valid.png (under 500KB) |
| Oversized icon file | icon-large.png (over 500KB) |
| Invalid format file | icon-invalid.txt or icon-invalid.pdf |
| Agent Name (for visibility test) | Icon Test Agent |
| Version name | Version 2 |

---

## Steps

### Part 1: Upload and Validation

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new skill with Name "Icon Test Skill", Description "Skill for testing icon functionality", Instructions "Test instructions for icon skill" | Skill is created successfully with default icon |
| 2 | Open the skill "Icon Test Skill" | Skill editor page loads |
| 3 | Click on the icon upload area or "Change Icon" button | Icon upload interface opens (file picker or drag-drop area) |
| 4 | Upload a valid PNG file under 500KB (e.g., icon-valid.png) | Icon upload succeeds; preview shows the new icon |
| 5 | Click Save | Skill is saved with the new custom icon |
| 6 | Verify the custom icon is displayed in the skill editor | Custom icon is visible in the editor |
| 7 | Open the skill again and attempt to upload a JPG file under 500KB | JPG file is accepted and uploaded successfully |
| 8 | Save and verify JPG icon is displayed | JPG icon is saved and displayed |

### Part 2: File Size Validation (Oversized File Rejection)

| # | Action | Expected Result |
|---|--------|-----------------|
| 9 | With the skill still open, attempt to upload an oversized file (e.g., icon-large.png over 500KB) | Upload is rejected with error message |
| 10 | Verify error message indicates file size limit "File must be under 500KB" or similar | Clear error message is displayed |
| 11 | Verify the previous valid icon remains unchanged | Previous icon is still displayed; oversized icon was not applied |

### Part 3: Invalid Format Rejection

| # | Action | Expected Result |
|---|--------|-----------------|
| 12 | Attempt to upload an invalid file format (e.g., .txt or .pdf) | Upload is rejected with error message |
| 13 | Verify error message indicates "Unsupported format. Use PNG, JPG, GIF, or WEBP" or similar | Clear error message is displayed |
| 14 | Verify the previous valid icon remains unchanged | Previous icon is still displayed |

### Part 4: Delete Icon (Revert to Default)

| # | Action | Expected Result |
|---|--------|-----------------|
| 15 | With the skill still open and custom icon displayed, click "Delete Icon" or "Remove Icon" button | Confirmation dialog appears (if applicable) |
| 16 | Confirm deletion | Custom icon is removed |
| 17 | Verify the skill reverts to the default icon | Default icon is displayed in the editor |
| 18 | Click Save | Skill is saved with default icon |
| 19 | Navigate to Skills list and verify default icon is displayed on the card | Default icon is shown on the skill card |

### Part 5: Visibility Across UI

| # | Action | Expected Result |
|---|--------|-----------------|
| 20 | Upload a new custom icon to the skill "Icon Test Skill" and save | Custom icon is uploaded and saved |
| 21 | Navigate to Skills list (Card view) and verify custom icon is displayed on the skill card | Custom icon is visible in CardList |
| 22 | Click on the skill to open detail page and verify custom icon is displayed in the header or detail area | Custom icon is visible on detail page |
| 23 | Create an Agent "Icon Test Agent" and attach the skill "Icon Test Skill" | Skill is attached to the agent |
| 24 | Open the Agent and verify the custom icon is displayed in the attached skills list (SkillCard) | Custom icon is visible in SkillCard on agent page |
| 25 | Open the skill attachment menu or SkillMenu and verify custom icon is displayed | Custom icon is visible in SkillMenu |
| 26 | In a chat or agent conversation, type `~` to trigger skill autocomplete | Skill autocomplete list appears |
| 27 | Verify the custom icon is displayed next to "Icon Test Skill" in the autocomplete list | Custom icon is visible in ~mention autocomplete |

### Part 6: Icon Persistence Across Versions

| # | Action | Expected Result |
|---|--------|-----------------|
| 28 | With the skill "Icon Test Skill" open and custom icon displayed, click "Save As Version" or create a new version | Version creation dialog appears |
| 29 | Name the new version "Version 2" and save | Version 2 is created |
| 30 | Verify the custom icon is displayed in Version 2 editor | Custom icon persisted to the new version |
| 31 | Navigate to Skills list and switch to Version 2 (if version switcher is available) | Version 2 is selected |
| 32 | Verify the custom icon is displayed on the Version 2 card | Custom icon persisted across version |
| 33 | Open Version 2 detail page and verify custom icon is displayed | Custom icon is visible on Version 2 |
| 34 | Switch back to base version and verify custom icon is still displayed there as well | Custom icon is present in both versions |

---

## Expected Final State

- Custom icons can be uploaded in PNG, JPG, GIF, and WEBP formats
- Files over 500KB are rejected with clear error message
- Invalid formats are rejected with clear error message
- Icon deletion reverts skill to default icon
- Custom icons display correctly in: Skills list CardList, skill detail page, agent SkillCard, SkillMenu, and ~mention autocomplete
- Custom icons persist across skill versions
- All icon operations complete successfully without data loss

---

## Pass/Fail Criteria

**Pass:**
- PNG, JPG, GIF, and WEBP files under 500KB upload successfully
- Files over 500KB are rejected with clear error message
- Invalid file formats are rejected with clear error message
- Icon deletion reverts to default icon and persists
- Custom icon is visible in: CardList, detail page, SkillCard (agent), SkillMenu, ~mention autocomplete
- Custom icon persists when creating new version
- Icon changes persist across save, navigation, and reload

**Fail:**
- Valid image formats are rejected
- Oversized files are accepted (no size validation)
- Invalid formats are accepted
- Icon deletion fails or does not revert to default
- Custom icon is missing in any UI location (list, detail, agent, menu, autocomplete)
- Custom icon does not persist across versions
- Any step produces an error or unexpected result

---

## Notes

**Source functional tests:** ELITEA-2604, ELITEA-2605, ELITEA-2606

**Regression rationale:** Consolidated from 3 tests covering icon functionality: (1) ELITEA-2604 tests upload and validation (format, size, delete), (2) ELITEA-2605 tests visibility across UI (list, detail, agent, menu, autocomplete), and (3) ELITEA-2606 tests persistence across versions. These tests cover the complete icon lifecycle and can be merged into a single comprehensive icon test.

**Selected checkpoints:**
- Upload PNG, JPG → success
- Upload oversized file → rejected with error
- Upload invalid format → rejected with error
- Delete icon → reverts to default
- Icon visible in: CardList, detail page, SkillCard, SkillMenu, autocomplete
- Create version → icon persists to new version
