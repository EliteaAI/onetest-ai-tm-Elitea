---
id: ELITEA-0158
title: Regression - Verify Editor Notes Field Remains Editable and Saveable
module: Agent Management
feature: Agent Configuration
priority: high
status: draft
tags:
  - feat:agents
  - eng:configuration
  - regression
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
---

## Test Case Summary

Verify that changes to export and fork functionality do not affect the core Editor Notes editing capability in agent configuration page. Editor Notes should remain fully editable, saveable, and retrievable.

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- User has permission to create and modify agents

## Test Data

| Test | Value |
|------|-------|
| Initial Value | "Initial editor notes for regression test" |
| Updated Value | "Updated editor notes after save" |
| Clear Test | (empty) |
| Re-enter Value | "Re-entered after clearing" |

## Test Steps

### Phase 1: Create Agent with Editor Notes

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to Agents page | Page loads |
| 2 | Click "New Agent" or equivalent | Agent creation form appears |
| 3 | Enter agent name "QA Editor Notes Regression" | Name entered |
| 4 | Scroll to Editor Notes section | Section visible |
| 5 | Verify field is editable (not disabled) | ✅ Field accepts input |
| 6 | Click into Editor Notes field | Field focused, cursor visible |
| 7 | Type "Initial editor notes for regression test" | Text appears in field as typed |
| 8 | Verify character input responsive | ✅ No lag or issues |
| 9 | Click Save button | Save initiated |
| 10 | Verify save success message | Success notification shown |
| 11 | Record agent ID/URL | ID recorded |

### Phase 2: Verify Persistence After Save

| Step | Action | Expected Result |
|------|--------|----------------|
| 12 | Reload browser page | Page reloads |
| 13 | Verify agent page loads | Agent configuration displayed |
| 14 | Scroll to Editor Notes section | Section visible |
| 15 | Verify Editor Notes field populated | Shows: "Initial editor notes for regression test" |
| 16 | Verify exact text match | ✅ No truncation or modification |

### Phase 3: Edit Existing Editor Notes

| Step | Action | Expected Result |
|------|--------|----------------|
| 17 | Click into Editor Notes field | Field focused |
| 18 | Select all text (Ctrl+A / Cmd+A) | All text selected |
| 19 | Type "Updated editor notes after save" | Old text replaced with new |
| 20 | Verify new text visible | Shows updated text |
| 21 | Click Save button | Save initiated |
| 22 | Verify save success | Success notification shown |
| 23 | Reload page | Page reloads |
| 24 | Verify Editor Notes updated | Shows: "Updated editor notes after save" |

### Phase 4: Clear Editor Notes

| Step | Action | Expected Result |
|------|--------|----------------|
| 25 | Click into Editor Notes field | Field focused |
| 26 | Select all text and delete (Backspace/Delete) | Field becomes empty |
| 27 | Verify field empty | No text visible |
| 28 | Click Save button | Save initiated |
| 29 | Verify save success | Success notification shown |
| 30 | Reload page | Page reloads |
| 31 | Verify Editor Notes empty | Field blank |

### Phase 5: Re-enter Editor Notes

| Step | Action | Expected Result |
|------|--------|----------------|
| 32 | Click into empty Editor Notes field | Field focused |
| 33 | Type "Re-entered after clearing" | Text appears |
| 34 | Click Save button | Save initiated |
| 35 | Verify save success | Success notification shown |
| 36 | Reload page | Page reloads |
| 37 | Verify Editor Notes shows new value | Shows: "Re-entered after clearing" |

### Phase 6: Navigation and Return

| Step | Action | Expected Result |
|------|--------|----------------|
| 38 | Navigate to Agents list page | List page loads |
| 39 | Navigate back to test agent | Agent page loads |
| 40 | Verify Editor Notes still present | Shows: "Re-entered after clearing" |
| 41 | Verify field still editable | Can click and modify text |

## Expected Results

- ✅ Editor Notes field is editable (not disabled or read-only)
- ✅ Text input is responsive and immediate
- ✅ Save operation succeeds
- ✅ Saved values persist after page reload
- ✅ Edit operation works on existing values
- ✅ Clear operation works (can save empty notes)
- ✅ Re-enter operation works after clearing
- ✅ Values persist across navigation
- ✅ Field remains editable throughout all operations

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All CRUD operations on Editor Notes field work correctly without any issues

**FAIL:** Any of the following:
- Field disabled or read-only
- Cannot enter text
- Cannot modify existing text
- Save fails
- Values not persisted
- Cannot clear field
- Any error during any operation
- Field becomes unusable at any point

## Notes

- Critical regression test to ensure core functionality not broken
- Tests complete CRUD cycle: Create, Read, Update, Delete (clear)
- Editor Notes editing is a foundational feature - must work flawlessly
- If this test fails, export/fork features are irrelevant

