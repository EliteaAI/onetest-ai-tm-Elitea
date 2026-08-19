---
id: ELITEA-0156
title: Regression - Verify Other Export Metadata Fields Not Affected by Editor Notes Addition
module: Agent Management
feature: Agent Export
priority: high
status: draft
tags:
  - feat:agents
  - eng:export
  - regression
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
---

## Test Case Summary

Verify that the addition of the `notes` field to agent export does not cause regression in other existing export fields (model, step_limit, welcome_message, chat_starters, instructions, description, etc.).

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- User has permission to create, configure, export, and import agents

## Test Data

**Complete Agent Configuration:**

| Field | Value |
|-------|-------|
| Name | QA Regression Test Agent |
| Description | "Complete agent for regression testing export metadata fields" |
| Model | gpt-5.4-mini |
| Step Limit | 25 |
| Instructions | "You are a helpful QA testing agent. Follow user instructions carefully." |
| Welcome Message | "Hello! I'm ready to assist with QA testing tasks." |
| Chat Starters | ["Help me test a feature", "Review test results", "Generate test data"] |
| Editor Notes | "Regression test - verify all fields export correctly" |
| Tags | qa, testing, regression |

## Test Steps

### Phase 1: Create Fully Configured Agent

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Create new agent with name "QA Regression Test Agent" | Agent created |
| 2 | Fill in Description field with test data | Description saved |
| 3 | Set Model to "gpt-5.4-mini" | Model selected |
| 4 | Set Step Limit to 25 | Step limit saved |
| 5 | Enter Instructions text | Instructions saved |
| 6 | Enter Welcome Message | Welcome message saved |
| 7 | Add 3 Chat Starters | Chat starters saved |
| 8 | Add tags: qa, testing, regression | Tags saved |
| 9 | Enter Editor Notes | Editor Notes saved |
| 10 | Click Save | Agent fully configured and saved |

### Phase 2: Export Agent

| Step | Action | Expected Result |
|------|--------|----------------|
| 11 | Export agent to `.md` file | Export succeeds, file downloads |
| 12 | Open exported file in text editor | File opens successfully |

### Phase 3: Verify All Fields Present in Export

| Step | Field Name | Expected Value | Status |
|------|-----------|----------------|--------|
| 13 | name | "QA Regression Test Agent" | ✅ Present |
| 14 | description | "Complete agent for regression testing..." | ✅ Present |
| 15 | model | "gpt-5.4-mini" | ✅ Present |
| 16 | step_limit | 25 | ✅ Present |
| 17 | instructions | "You are a helpful QA testing agent..." | ✅ Present |
| 18 | welcome_message | "Hello! I'm ready to assist..." | ✅ Present |
| 19 | chat_starters | Array with 3 items | ✅ Present |
| 20 | tags | ["qa", "testing", "regression"] | ✅ Present |
| 21 | notes | "Regression test - verify all fields..." | ✅ Present (NEW) |

### Phase 4: Verify Field Values Correct

| Step | Action | Expected Result |
|------|--------|----------------|
| 22 | Compare description in file vs UI | ✅ Exact match |
| 23 | Compare model in file vs UI | ✅ Exact match |
| 24 | Compare step_limit in file vs UI | ✅ Exact match |
| 25 | Compare instructions in file vs UI | ✅ Exact match |
| 26 | Compare welcome_message in file vs UI | ✅ Exact match |
| 27 | Compare chat_starters array | ✅ All 3 starters present and correct |
| 28 | Compare tags array | ✅ All 3 tags present |
| 29 | Compare notes field | ✅ Matches Editor Notes |

### Phase 5: Re-Import and Verify

| Step | Action | Expected Result |
|------|--------|----------------|
| 30 | Import the exported file | Import succeeds |
| 31 | Open imported agent | Agent page loads |
| 32 | Verify Description | ✅ Matches original |
| 33 | Verify Model | ✅ Matches original |
| 34 | Verify Step Limit | ✅ Matches original |
| 35 | Verify Instructions | ✅ Matches original |
| 36 | Verify Welcome Message | ✅ Matches original |
| 37 | Verify Chat Starters count | ✅ 3 starters present |
| 38 | Verify Chat Starters content | ✅ All match original |
| 39 | Verify Tags | ✅ All tags match original |
| 40 | Verify Editor Notes | ✅ Matches original |

## Expected Results

- ✅ All existing fields present in exported file
- ✅ All field values correct in exported file
- ✅ New `notes` field present alongside existing fields
- ✅ File structure valid and parseable
- ✅ Re-import succeeds and populates all fields correctly
- ✅ No data loss or corruption in any field
- ✅ No regression in export/import functionality

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All existing fields export correctly with correct values, and import restores all fields accurately

**FAIL:** Any of the following:
- Any existing field missing from export
- Any field value incorrect or corrupted
- Import fails
- Any field not restored correctly during import
- Any data loss detected

## Notes

- Critical regression test to ensure new feature doesn't break existing functionality
- Test all major agent configuration fields
- Verify complete export → import cycle
- Compare exported file structure to previous exports (if available) to ensure consistency

