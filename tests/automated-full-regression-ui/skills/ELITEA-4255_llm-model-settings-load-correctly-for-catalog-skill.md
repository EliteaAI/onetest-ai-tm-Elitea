---
id: ELITEA-4255
title: LLM Model/Settings section loads for Catalog skill in chat
priority: critical
type: regression
module: elitea-platform
status: draft
execution_type: manual
tags: [feat:skills, catalog, chat, model-settings, bug-7219, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922, EliteaAI/elitea_issues#7219]
---
# ELITEA-4255: LLM Model/Settings section loads for Catalog skill in chat (Regression)

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that LLM Model/Settings section loads correctly for Catalog skill participant in chat (Bug fix for #7219: "Failed to load configuration" error).

**Coverage:**
- LLM Model/Settings section loads successfully
- NO "Failed to load configuration" error
- Model chip displays configured model
- Settings are visible
- Bug #7219 is fixed and stays fixed

## Preconditions

- User is logged in to {{base_url}}
- Chat with Catalog skill participant is open
- Catalog skill has configured LLM model and settings (e.g., "skill-publishing-test")

## Test Data

- Catalog skill: "skill-publishing-test" (from bug #7219) or any published skill
- Expected: Model/Settings load without error, display configured model

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create chat with Catalog skill via Run button | Chat opens with skill as participant |
| 2 | Observe right panel "PARTICIPANTS" section | Right panel shows "SKILLS" section with skill participant |
| 3 | Look for "Context Management" or "LLM Settings" section | Context Management section is visible |
| 4 | Check the LLM Model/Settings section | **BUG FIX #7219:** Section loads successfully, NO "Failed to load configuration" error message |
| 5 | Observe the model chip/selector | Model chip displays the skill's configured model name (e.g., "Dial-Anthropic-Sonnet-5.5") |
| 6 | Check for additional settings display | Temperature, max tokens, and other LLM settings are visible |
| 7 | Verify settings match skill configuration | Displayed settings match the published skill's configured LLM settings |
| 8 | Compare with screenshot from bug #7219 | Error message "Failed to load configuration" does NOT appear (bug is fixed) |

## Expected Final State

LLM Model/Settings section loads successfully; model chip shows configured model; no error messages.

## Pass/Fail Criteria

**Pass:** LLM Model/Settings section loads without "Failed to load configuration" error; model and settings display correctly.

**Fail:** "Failed to load configuration" error appears, or model/settings fail to load.

## Notes

This regression test specifically verifies the fix for bug #7219 remains stable across releases.
