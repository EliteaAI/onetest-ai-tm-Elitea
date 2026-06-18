---
id: ELITEA-0198
title: "TC-015: Clicking Continue Triggers Automatic AI Validation With Loading Spinner and \"Excluding Components\" Progress Text"
priority: critical
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0198: TC-015: Clicking Continue Triggers Automatic AI Validation With Loading Spinner and "Excluding Components" Progress Text

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking Continue on the Preparation step automatically transitions to the AI Validation step, shows a loading spinner with percentage progress, displays informational text and "Excluding components..." sub-text confirming snapshot exclusion is running, and keeps the Continue button disabled throughout.

Coverage:
- Clicking Continue on Preparation auto-triggers the Validation step (not user-driven)
- Stepper advances to "Validation" as the active step
- Loading spinner with percentage indicator shown
- Main text: "Reviewing your agent version to ensure it meets publication rules. It takes up to 30 seconds – you'll see results shortly!"
- Sub-text: "Excluding components..." confirms snapshot exclusion is processing
- Continue button disabled during loading — user cannot skip or advance manually
- Validation completes within approximately 30 seconds

## Preconditions

- Logged in as User A
- Agent A is fully configured with no critical issues; has at least one saved version
- Publish modal is open at the Preparation step with version name filled and checkbox checked

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | On the Preparation step, verify version name is filled and 'I agree with the Publishing Terms.' is checked | Continue button is cyan and enabled |
| 2 | Click Continue | Stepper active step transitions from 'Preparation' to 'Validation' |
| 3 | Observe the modal content immediately after clicking Continue | A circular loading spinner appears with a percentage indicator (e.g., 75%) |
| 4 | Read the primary instructional text shown during loading | 'Reviewing your agent version to ensure it meets publication rules. It takes up to 30 seconds – you’ll see results shortly!' |
| 5 | Read the sub-text below the main message | Sub-text 'Excluding components...' is visible, confirming external toolkits/MCPs/Pipelines are being excluded from the snapshot |
| 6 | Attempt to click Continue while the spinner is active | Continue button is greyed out and does not respond — user cannot manually advance |
| 7 | Wait for validation to complete | Spinner disappears; validation results appear (banner + SUMMARY section); Publish button (enabled or disabled) shown in place of Continue |

## Expected Final State

Spinner disappears; validation results appear (banner + SUMMARY section); Publish button (enabled or disabled) shown in place of Continue

## Pass/Fail Criteria

PASS:
- Validation step activates automatically when Continue is clicked — no additional user input required
- Loading spinner with percentage shown during the validation process
- "Excluding components..." sub-text is visible during processing
- Continue button is disabled throughout loading; user cannot bypass the validation step
- Validation finishes and results appear within ~30 seconds

FAIL:
- Validation step does not auto-trigger — user must take extra actions to start validation
- No spinner or progress indicator shown during validation
- "Excluding components..." text is absent
- Continue button is clickable during loading, allowing the user to skip validation
- Validation hangs indefinitely or takes over 60 seconds without completing
