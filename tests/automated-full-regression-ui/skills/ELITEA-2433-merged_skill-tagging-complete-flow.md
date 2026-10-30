---
id: ELITEA-2433
title: "Skill — Tagging (Complete Flow)"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, regression:merged]
requirements: []
---

# ELITEA-2433: Skill — Tagging (Complete Flow)

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify complete tag management workflow for skills including adding single and multiple tags on creation and after creation, verifying persistence, and removing tags. Success is confirmed when all tag operations work correctly and persist across saves and reloads.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill Name 1 | Single Tag Test Skill |
| Skill Description 1 | Skill for testing single tag operations |
| Tag 1 | regression-v1 |
| Skill Name 2 | Multi Tag Test Skill |
| Skill Description 2 | Skill for testing multiple tags |
| Tags on creation | api, automation, regression |
| Additional tag | integration |

---

## Steps

### Part 1: Add and Remove Single Tag

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new skill with Name "Single Tag Test Skill" and Description "Skill for testing single tag operations" (no tags initially) | Skill is created successfully without tags |
| 2 | Open the skill "Single Tag Test Skill" | Skill editor page loads |
| 3 | Add tag "regression-v1" using the tags input field | Tag "regression-v1" is added to the skill |
| 4 | Click Save | Skill is saved successfully |
| 5 | Navigate to Skills list and verify the tag "regression-v1" appears on the skill card | Tag is visible on the skill card |
| 6 | Re-open the skill "Single Tag Test Skill" | Skill editor page loads |
| 7 | Verify tag "regression-v1" is present in the tags field | Tag persisted correctly after save/reload |
| 8 | Remove tag "regression-v1" by clicking the X or delete button on the tag | Tag is removed from the tags field |
| 9 | Click Save | Skill is saved successfully |
| 10 | Navigate to Skills list and verify the tag "regression-v1" no longer appears on the card | Tag has been removed and is not displayed |
| 11 | Re-open the skill to verify tag is permanently removed | Tag is not present in the tags field |

### Part 2: Multiple Tags on Creation

| # | Action | Expected Result |
|---|--------|-----------------|
| 12 | Navigate to Create Skill page | Create Skill page loads |
| 13 | Fill in Name "Multi Tag Test Skill" and Description "Skill for testing multiple tags" | Mandatory fields are filled |
| 14 | Add multiple tags "api", "automation", "regression" during creation | All three tags are added to the tags field |
| 15 | Click Save | Skill is created successfully |
| 16 | Navigate to Skills list and verify all three tags ("api", "automation", "regression") appear on the skill card | All tags are visible on the card |
| 17 | Re-open the skill "Multi Tag Test Skill" | Skill editor page loads |
| 18 | Verify all three tags are present in the tags field | All tags persisted correctly |

### Part 3: Add Tags After Creation

| # | Action | Expected Result |
|---|--------|-----------------|
| 19 | With the skill "Multi Tag Test Skill" still open, add an additional tag "integration" | New tag is added to the existing tags |
| 20 | Click Save | Skill is saved successfully |
| 21 | Navigate to Skills list and verify all four tags ("api", "automation", "regression", "integration") appear on the card | All four tags are visible |
| 22 | Re-open the skill and verify all four tags persist | All tags are present after reload |

---

## Expected Final State

- Single tag can be added to a skill and persists correctly
- Tag removal works correctly and persists
- Multiple tags can be added during skill creation and all persist
- Additional tags can be added after creation and persist alongside existing tags
- All tag operations reflect correctly in Skills list card view and in skill editor after save/reload

---

## Pass/Fail Criteria

**Pass:**
- Single tag "regression-v1" is added, persists, can be viewed on card, and is successfully removed
- Multiple tags can be added during skill creation and all persist correctly
- Additional tags can be added after creation without affecting existing tags
- All tag operations persist across save, navigation, and reload
- Tags display correctly on skill cards in the list view

**Fail:**
- Any tag operation (add/remove) fails or does not persist
- Tags do not appear on skill cards after save
- Tags are lost after navigation or reload
- Multiple tags cannot be added or saved together
- Any step produces an error or unexpected result

---

## Notes

**Source functional tests:** ELITEA-2433, ELITEA-2434

**Regression rationale:** Consolidated from 2 tests covering tag management at different scales: (1) single tag add/remove operations with persistence verification, and (2) multiple tags on creation and after creation. These tests cover the same tag management functionality and can be merged into a single comprehensive tagging test that covers both single and multiple tag scenarios.

**Selected checkpoints:**
- Single tag add → persists → visible on card → remove → persists (not visible)
- Multiple tags on creation → all persist → all visible on card
- Add tag after creation → persists with existing tags
