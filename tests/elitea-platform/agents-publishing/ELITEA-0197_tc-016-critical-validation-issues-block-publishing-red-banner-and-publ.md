---
id: ELITEA-0197
title: "TC-016: Critical Validation Issues Block Publishing — Red Banner and Publish Button Disabled"
priority: critical
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, execution, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0197: TC-016: Critical Validation Issues Block Publishing — Red Banner and Publish Button Disabled

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when AI validation detects critical issues (missing description, variable with no default value), a red failure banner is shown, the SUMMARY section displays Critical > 0, the Publish button is greyed out and non-interactive, and the Summary Details popup provides actionable Field / Issue / Fix guidance for each critical item.

Coverage:
- Red banner: "Sorry, your agent version doesn't meet all the necessary requirements. Follow summary details to fix the issues and try again."
- SUMMARY section shows Critical count > 0
- Publish button is disabled (greyed out, not clickable) when Critical > 0
- Summary Details popup lists each critical issue with: title, Field, Issue description, Fix instruction
- Specific checks: empty description → "Agent Description is missing"; empty variable default → "Variable has no value"
- After fixing critical issues and re-running, Publish button becomes enabled

## Preconditions

- Logged in as User A
- Agent D prepared with intentional critical deficiencies:
  * Description field: left empty
  * Variable 'api_endpoint' added with no default value set
  * Instructions and name filled; has at least a "base" saved version

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Publish modal on Agent D; enter a valid unique version name; check 'I agree with the Publishing Terms.' | Preparation step complete; Continue button enabled |
| 2 | Click Continue | Validation step auto-triggers; loading spinner shown; 'Excluding components...' visible |
| 3 | Wait for validation to complete | Results appear on the Validation step |
| 4 | Observe the banner color and message | Red banner: 'Sorry, your agent version doesn’t meet all the necessary requirements. Follow summary details to fix the issues and try again.' |
| 5 | Check the SUMMARY section | Critical count is > 0 (e.g., Critical: 4); Warnings and Suggestions may also be present |
| 6 | Observe the Publish button | Publish button is greyed out and disabled — cannot be clicked |
| 7 | Attempt to click the Publish button | No action — button does not respond |
| 8 | Click the expand icon on SUMMARY DETAILS | Summary Details popup opens with Critical issues section |
| 9 | Find the 'Agent Description is missing' entry | Entry shows: Field: Description / Issue: Description field is empty / Fix: Add a clear description of what your agent does |
| 10 | Find the 'Variable api_endpoint has no value' entry | Entry shows: Field: Variables → api_endpoint / Issue: Default value is empty / Fix: Provide a default value for this variable |
| 11 | Close modal. Fix Agent D: add description text and a default value for api_endpoint. Re-open Publish modal, enter new version name, re-run validation. | Validation passes; Publish button is now enabled |

## Expected Final State

Validation passes; Publish button is now enabled

## Pass/Fail Criteria

PASS:
- Red banner displayed with the exact failure message
- SUMMARY shows Critical > 0
- Publish button is disabled (not clickable) when Critical > 0 — critical validation acts as a hard gate
- Summary Details popup lists "Agent Description is missing" and "Variable has no value" with Field / Issue / Fix details
- After fixing critical issues, Publish button becomes enabled

FAIL:
- Red banner not shown despite critical issues existing
- Publish button remains enabled when Critical > 0 (gate bypassed)
- Summary Details does not show structured Field / Issue / Fix detail for each critical item
- After fixing issues, Publish button remains disabled
