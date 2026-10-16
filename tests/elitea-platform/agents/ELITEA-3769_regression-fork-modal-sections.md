---
id: ELITEA-3769
title: Regression - Verify Other Fork Modal Sections Not Affected by Editor Notes Addition
module: Agent Management
feature: Agent Fork
priority: high
status: draft
tags:
  - feat:agents
  - eng:fork
  - regression
  - ui
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
---

## Test Case Summary

Verify that the addition of the EDITOR NOTES section to the Fork Parameters modal does not cause regression in other existing modal sections (DESCRIPTION, INSTRUCTIONS, WELCOME MESSAGE, CHAT STARTERS, OTHER).

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- At least one fully configured agent exists with all fields populated
- User has permission to fork agents

## Test Data

**Source Agent Configuration:**

| Field | Value |
|-------|-------|
| Name | QA Fork Modal Regression Agent |
| Description | "Regression test agent for fork modal functionality" |
| Instructions | "You are a QA testing agent. Follow all test protocols and document findings." |
| Welcome Message | "Welcome! Ready to begin QA testing." |
| Chat Starters | ["Start regression test", "Verify fork functionality", "Check modal sections"] |
| Editor Notes | "Fork modal regression verification" |

## Test Steps

### Phase 1: Open Fork Modal and Verify All Sections Present

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to source agent | Agent page loads |
| 2 | Verify all fields populated in agent | All configuration visible |
| 3 | Click Fork from agent menu | Fork Parameters modal opens |
| 4 | Click "Show details" | Details section expands |
| 5 | Locate DESCRIPTION section | ✅ Section visible |
| 6 | Locate INSTRUCTIONS section | ✅ Section visible |
| 7 | Locate WELCOME MESSAGE section | ✅ Section visible |
| 8 | Locate CHAT STARTERS section | ✅ Section visible |
| 9 | Locate EDITOR NOTES section | ✅ Section visible (NEW) |
| 10 | Locate OTHER section | ✅ Section visible |
| 11 | Verify no sections missing | ✅ All expected sections present |

### Phase 2: Verify Existing Section Content Correct

| Step | Section | Action | Expected Result |
|------|---------|--------|----------------|
| 12 | DESCRIPTION | Read content in modal | Displays: "Regression test agent for fork modal functionality" |
| 13 | DESCRIPTION | Compare to source agent | ✅ Exact match |
| 14 | INSTRUCTIONS | Read content in modal | Displays: "You are a QA testing agent..." |
| 15 | INSTRUCTIONS | Compare to source agent | ✅ Exact match |
| 16 | WELCOME MESSAGE | Read content in modal | Displays: "Welcome! Ready to begin QA testing." |
| 17 | WELCOME MESSAGE | Compare to source agent | ✅ Exact match |
| 18 | CHAT STARTERS | Count items in modal | Shows 3 starters |
| 19 | CHAT STARTERS | Read all starter texts | All 3 match source agent |
| 20 | OTHER | Check Step Limit display | Shows: "Step Limit: 25" or equivalent |
| 21 | EDITOR NOTES | Read content in modal | Displays: "Fork modal regression verification" |

### Phase 3: Test Existing Section Interactive Behavior

| Step | Action | Expected Result |
|------|--------|----------------|
| 22 | Test expand/collapse on DESCRIPTION (if applicable) | ✅ Works correctly |
| 23 | Test expand/collapse on INSTRUCTIONS (if applicable) | ✅ Works correctly |
| 24 | Test expand/collapse on WELCOME MESSAGE (if applicable) | ✅ Works correctly |
| 25 | Test expand/collapse on CHAT STARTERS (if applicable) | ✅ Works correctly |
| 26 | Test expand/collapse on EDITOR NOTES (if applicable) | ✅ Works correctly |
| 27 | Test expand/collapse on OTHER (if applicable) | ✅ Works correctly |
| 28 | Scroll through modal | All sections accessible, no layout breaks |

### Phase 4: Complete Fork Operation and Verify

| Step | Action | Expected Result |
|------|--------|----------------|
| 29 | Select target project | Project selected |
| 30 | Click Fork button | Fork initiated |
| 31 | Wait for fork to complete | Fork succeeds |
| 32 | Navigate to forked agent | Forked agent page loads |
| 33 | Verify Description carried over | ✅ Matches source |
| 34 | Verify Instructions carried over | ✅ Matches source |
| 35 | Verify Welcome Message carried over | ✅ Matches source |
| 36 | Verify Chat Starters carried over | ✅ All 3 starters match |
| 37 | Verify Step Limit carried over | ✅ Matches source |
| 38 | Verify Editor Notes carried over | ✅ Matches source |
| 39 | Verify no data loss in any field | ✅ All fields correct |

### Phase 5: Test Modal Reopening After Navigation

| Step | Action | Expected Result |
|------|--------|----------------|
| 40 | Navigate back to source agent | Agent page loads |
| 41 | Open Fork modal again | Modal opens |
| 42 | Verify all sections still present | ✅ All sections visible |
| 43 | Verify content still correct | ✅ No corruption or loss |
| 44 | Close modal | Modal closes cleanly |

## Expected Results

- ✅ Fork Parameters modal opens correctly
- ✅ All existing sections (DESCRIPTION, INSTRUCTIONS, WELCOME MESSAGE, CHAT STARTERS, OTHER) present
- ✅ New EDITOR NOTES section present
- ✅ All section content displays correctly
- ✅ All section content matches source agent values
- ✅ Interactive behavior (expand/collapse) works for all sections
- ✅ Fork operation succeeds
- ✅ All fields correctly carried over to forked agent
- ✅ No data loss or corruption

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All existing modal sections function correctly with correct content, and fork operation succeeds

**FAIL:** Any of the following:
- Any existing section missing from modal
- Any section content incorrect or missing
- Interactive behavior broken on any section
- Fork operation fails
- Any field not carried over correctly
- Layout or display issues

## Notes

- Critical regression test for Fork modal UI
- Ensures new EDITOR NOTES section doesn't break existing modal functionality
- Test on multiple browsers if possible (Chrome, Firefox, Safari)
- Verify modal remains scrollable and all sections accessible

