---
id: ELITEA-0203
title: "TC-003: Continue Button Activates Only When Version Name + \"I Agree\" Are Both Provided"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0203: TC-003: Continue Button Activates Only When Version Name + "I Agree" Are Both Provided

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Continue" button on the Preparation step transitions from disabled to enabled only when both a version name is entered AND the "I agree with the Publishing Terms." checkbox is checked — not from either condition alone.

Coverage:
- Empty version name + unchecked → Continue disabled
- Version name filled + unchecked → Continue disabled
- Empty version name + checked → Continue disabled
- Version name filled + checked → Continue enabled
- Unchecking checkbox after enabling → Continue reverts to disabled

## Preconditions

- Logged in as User A
- "Publish version" modal is open on Agent A (Preparation step)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the 'Publish version' modal on Agent A | Modal opens; Version name empty, 'I agree with the Publishing Terms.' unchecked, Continue disabled |
| 2 | Leave Version name empty; leave checkbox unchecked | Continue button remains disabled |
| 3 | Type 'v1.0' in Version name; leave checkbox unchecked | Continue button remains disabled |
| 4 | Clear Version name field; check 'I agree with the Publishing Terms.' | Continue button remains disabled |
| 5 | Type 'v1.0' in Version name AND check 'I agree with the Publishing Terms.' | Continue button becomes enabled (active, clickable) |
| 6 | Uncheck 'I agree with the Publishing Terms.' (Version name still 'v1.0') | Continue button reverts to disabled |
| 7 | Re-check 'I agree with the Publishing Terms.' | Continue button re-enables |

## Expected Final State

Continue button re-enables

## Pass/Fail Criteria

PASS:
- Continue button is disabled in states 1–4
- Continue button is enabled only when both version name is entered AND checkbox is checked
- Continue button re-disables when checkbox is unchecked

FAIL:
- Continue button activates without the checkbox being checked
- Continue button activates without a version name entered
- Continue button stays disabled even when both conditions are met
