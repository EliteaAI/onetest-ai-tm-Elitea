---
id: ELITEA-0150
title: Fork Backend - Verify Editor Notes Carried Over to Forked Agent
module: Agent Management
feature: Agent Fork
priority: critical
status: draft
tags:
  - feat:agents
  - eng:fork
  - editor-notes
  - backend
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
acceptance_criteria: AC2 - Editor Notes value correctly carried over after fork
---

## Test Case Summary

Verify that when an agent with Editor Notes is forked, the forked agent inherits the exact Editor Notes value from the source agent (backend carryover functionality).

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- At least one agent exists with non-empty Editor Notes field
- User has permission to fork agents and create new agents

## Test Data

| Field | Value |
|-------|-------|
| Source Agent Name | QA Source Agent - Carryover Test |
| Editor Notes | "Backend carryover validation test" |
| Fork Target Project | Private |

## Test Steps

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to Agents page in Private project | Agents list page loads |
| 2 | Open source agent "QA Source Agent - Carryover Test" | Agent details page displays |
| 3 | Scroll to Editor Notes section | Section visible |
| 4 | Verify Editor Notes value | Field shows: "Backend carryover validation test" |
| 5 | Note the agent ID/URL for reference | Agent ID recorded (e.g., `/agents/266`) |
| 6 | Click agent menu (⋮) → Fork | Fork Parameters modal opens |
| 7 | Verify PROJECT dropdown shows "Private" | Project selector visible |
| 8 | Select "Private" project (if not already selected) | Project selected |
| 9 | Verify other fork parameters displayed | DESCRIPTION, INSTRUCTIONS, etc. visible |
| 10 | Click "Fork" button | Fork operation initiated |
| 11 | Wait for fork to complete | Loading indicator appears then completes |
| 12 | Verify navigation to forked agent | Browser navigates to new agent page (different URL) |
| 13 | Verify forked agent page loaded | Agent details page displays for forked agent |
| 14 | Check agent name | Name shows as fork of source (e.g., "QA Source Agent - Carryover Test (forked)") |
| 15 | Scroll down to Editor Notes section | Section visible in forked agent |
| 16 | Verify Editor Notes field populated | Field is not empty |
| 17 | Verify Editor Notes value matches source | Value is: "Backend carryover validation test" |
| 18 | Compare character-by-character | Exact match with source agent's notes |
| 19 | Open source agent in new tab | Source agent page loads |
| 20 | Verify source agent notes unchanged | Still shows: "Backend carryover validation test" |

## Expected Results

- ✅ Fork operation completes successfully
- ✅ New forked agent created
- ✅ Navigation to forked agent page succeeds
- ✅ Editor Notes field populated in forked agent
- ✅ Editor Notes value exactly matches source: "Backend carryover validation test"
- ✅ Source agent Editor Notes unchanged

## Actual Results

_(To be filled during test execution)_

## Pass/Fail Criteria

**PASS:** All steps execute successfully and forked agent inherits exact Editor Notes value from source

**FAIL:** Any of the following:
- Fork operation fails
- Forked agent Editor Notes empty or null
- Editor Notes value incorrect or truncated
- Source agent Editor Notes modified during fork

## Notes

- This test validates AC2 backend carryover requirement
- Backend functionality should preserve notes during fork operation
- Linked PR: elitea_core #315
- Record both source and forked agent IDs for traceability

