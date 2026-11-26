---
id: ELITEA-2428
title: "Skill — CRUD (Create, Edit, Navigate, Validation)"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, regression:merged]
requirements: []
---

# ELITEA-2428: Skill — CRUD (Create, Edit, Navigate, Validation)

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify complete CRUD operations for skills including card view display, mandatory field validation, editing fields, and navigation. Success is confirmed when all CRUD operations work correctly and persist across navigations.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Initial Skill Name | Test Skill Alpha |
| Initial Skill Description | Initial description for testing |
| Initial Skill Instructions | Initial instructions content |
| Updated Skill Name | Test Skill Alpha Updated |
| Updated Skill Description | Updated description for testing |
| Updated Skill Instructions | Updated instructions content |
| Tag for testing | regression-v1 |

---

## Steps

### Part 1: Skills Listing — Card View Validation

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills list page | Skills list page loads successfully |
| 2 | Verify Card view is active by default | Card view is selected/active |
| 3 | Create a skill with name "Test Skill Alpha", description "Initial description for testing", instructions "Initial instructions content", and tag "regression-v1" | Skill is created successfully |
| 4 | Return to Skills list page and verify the skill card displays: skill icon (default or custom), skill name "Test Skill Alpha", tag "regression-v1" | All elements are visible on the card |
| 5 | Hover over the skill card and verify description "Initial description for testing" appears on hover | Description tooltip/hover text appears correctly |

### Part 2: Mandatory Fields Validation on Creation

| # | Action | Expected Result |
|---|--------|-----------------|
| 6 | Navigate to Create Skill page | Create Skill page loads successfully |
| 7 | Leave Name empty, fill in Description "Test desc" and Instructions "Test inst" | Fields are filled as specified |
| 8 | Verify Save button is inactive/disabled | Save button is disabled |
| 9 | Fill in Name "Validation Test", clear Description field, keep Instructions filled | Name is filled, Description is empty |
| 10 | Verify Save button is inactive/disabled | Save button is disabled |
| 11 | Clear both Name and Description fields | Both mandatory fields are empty |
| 12 | Verify Save button is inactive/disabled | Save button is disabled |
| 13 | Fill in both Name "Validation Test Skill" and Description "Valid description" | Both mandatory fields are filled |
| 14 | Verify Save button becomes active/enabled | Save button is enabled |
| 15 | Click Save | Skill is created successfully and appears in Skills list |

### Part 3: Edit Skill Fields

| # | Action | Expected Result |
|---|--------|-----------------|
| 16 | Open the skill "Test Skill Alpha" created in Part 1 | Skill editor page loads with current values |
| 17 | Update Name to "Test Skill Alpha Updated" | Name field is updated |
| 18 | Update Description to "Updated description for testing" | Description field is updated |
| 19 | Switch the Instructions section to Edit mode (click the "Edit mode" toggle; skill detail page opens in Preview), then update Instructions to "Updated instructions content" | Instructions field is updated |
| 20 | Click Save | Changes are saved successfully |
| 21 | Navigate back to Skills list using the back button | Navigation returns to Skills list (NOT to Chats page) |
| 22 | Re-open the skill "Test Skill Alpha Updated" | Skill editor page loads |
| 23 | Verify Name is "Test Skill Alpha Updated" | Name persisted correctly |
| 24 | Verify Description is "Updated description for testing" | Description persisted correctly |
| 25 | Verify Instructions are "Updated instructions content" | Instructions persisted correctly |

### Part 4: Navigation Verification

| # | Action | Expected Result |
|---|--------|-----------------|
| 26 | From Skills editor, click the Back button in the header | Navigation occurs |
| 27 | Verify navigation goes to Skills list page (NOT Chats page) | Skills list page is displayed |

---

## Expected Final State

- Skills list displays cards with correct icon, name, description (on hover), and tags
- Mandatory field validation prevents saving skills without Name or Description
- All edited skill fields (Name, Description, Instructions) persist correctly after save and reload
- Back button from Skills editor navigates to Skills list, not Chats page
- All CRUD operations complete successfully

---

## Pass/Fail Criteria

**Pass:**
- Card view displays all required elements correctly (icon, name, tags, description on hover)
- Save button is disabled when mandatory fields (Name or Description) are missing
- All field edits persist correctly after save and navigation
- Back button from Skills editor navigates to Skills list page

**Fail:**
- Any card view element is missing or displayed incorrectly
- Save button is enabled when mandatory fields are missing, or disabled when all mandatory fields are filled
- Any edited field does not persist after save
- Back button navigates to Chats page instead of Skills list
- Any step produces an error or unexpected result

---

## Notes

**Source functional tests:** ELITEA-2428, ELITEA-2429, ELITEA-2430, ELITEA-2431

**Regression rationale:** Consolidated from 4 tests covering sequential CRUD operations: (1) viewing skills list in card format with all required display elements, (2) validating mandatory fields prevent incomplete skill creation, (3) editing skill fields, and (4) navigation correctness. These operations naturally flow together as a complete CRUD workflow.

**Selected checkpoints:**
- Card view displays icon, name, description on hover, tags
- Save disabled without Name; Save disabled without Description; Save enabled when both present
- Name, Description, and Instructions edits all persist
- Back button goes to Skills list (not Chats)
