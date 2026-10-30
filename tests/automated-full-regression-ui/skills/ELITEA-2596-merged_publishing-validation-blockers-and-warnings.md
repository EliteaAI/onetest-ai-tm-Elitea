---
id: ELITEA-2596
title: "Skill — Publishing Validation (Blockers & Warnings)"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, feat:publishing, feat:validation, regression:merged]
requirements: []
---

# ELITEA-2596: Skill — Publishing Validation (Blockers & Warnings)

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that AI validation for skill publishing correctly identifies FAIL-status blockers (short content, placeholders, secrets) that prevent publishing, and WARN-status issues (generic name, missing icon) that allow publishing with warnings. Success is confirmed when blockers prevent publishing and warnings allow publishing with acknowledgment.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- User has permissions to publish skills.

---

## Test Data

| Field | Value |
|-------|-------|
| Blocker Test 1 - Short Content Skill Name | Short Content Skill |
| Blocker Test 1 - Instructions | Do X |
| Blocker Test 2 - Placeholder Skill Name | Placeholder Skill |
| Blocker Test 2 - Instructions | TODO: Add instructions here. This is a placeholder. |
| Blocker Test 3 - Secret Skill Name | Secret Skill |
| Blocker Test 3 - Instructions | Use API key: sk-proj-abc123xyz456 to authenticate |
| Warning Test 1 - Generic Name Skill Name | Skill |
| Warning Test 1 - Instructions | Provide detailed assistance on coding tasks. Help users debug code and suggest best practices. |
| Warning Test 2 - No Icon Skill Name | Well Described Skill |
| Warning Test 2 - Instructions | This skill provides comprehensive assistance with data analysis tasks. |

---

## Steps

### Part 1: FAIL Status Blockers — Short Content

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new skill with Name "Short Content Skill" | Skill is created successfully |
| 2 | Enter very short Instructions: "Do X" (insufficient content) | Instructions field contains short content |
| 3 | Save the skill | Skill is saved |
| 4 | Navigate to Publishing wizard (Publish button/menu) | Publishing wizard opens (Step 1: Details) |
| 5 | Fill in required publishing details (if any) and proceed to validation step | Validation step is reached |
| 6 | Click "Validate" or "Run AI Validation" | AI validation runs |
| 7 | Verify validation result shows FAIL status | Validation status is "FAIL" or equivalent blocker indicator |
| 8 | Verify error message indicates "content too short" or similar blocker reason | Error message describes the short content issue |
| 9 | Verify "Publish" or "Next" button is disabled/blocked | Cannot proceed to publish |
| 10 | Attempt to click Publish (if button is present) | Publishing is blocked; error message or disabled state prevents publish |

### Part 2: FAIL Status Blockers — Placeholder Content

| # | Action | Expected Result |
|---|--------|-----------------|
| 11 | Create a new skill with Name "Placeholder Skill" | Skill is created successfully |
| 12 | Enter Instructions: "TODO: Add instructions here. This is a placeholder." | Instructions contain placeholder text |
| 13 | Save the skill and navigate to Publishing wizard | Publishing wizard opens |
| 14 | Proceed to validation step and click "Validate" | AI validation runs |
| 15 | Verify validation result shows FAIL status | Validation status is "FAIL" |
| 16 | Verify error message indicates "placeholder detected" or similar blocker | Error message describes placeholder content issue |
| 17 | Verify publishing is blocked | Publish button is disabled or publishing step is blocked |

### Part 3: FAIL Status Blockers — Secrets Detected

| # | Action | Expected Result |
|---|--------|-----------------|
| 18 | Create a new skill with Name "Secret Skill" | Skill is created successfully |
| 19 | Enter Instructions: "Use API key: sk-proj-abc123xyz456 to authenticate" (contains secret pattern) | Instructions contain apparent secret |
| 20 | Save the skill and navigate to Publishing wizard | Publishing wizard opens |
| 21 | Proceed to validation step and click "Validate" | AI validation runs |
| 22 | Verify validation result shows FAIL status | Validation status is "FAIL" |
| 23 | Verify error message indicates "potential secret detected" or similar security blocker | Error message describes secret detection issue |
| 24 | Verify publishing is blocked | Publish button is disabled or publishing step is blocked |

### Part 4: WARN Status Allows Publishing — Generic Name

| # | Action | Expected Result |
|---|--------|-----------------|
| 25 | Create a new skill with Name "Skill" (generic/non-descriptive name) | Skill is created successfully |
| 26 | Enter Instructions: "Provide detailed assistance on coding tasks. Help users debug code and suggest best practices." (sufficient quality content) | Instructions are detailed and complete |
| 27 | Save the skill and navigate to Publishing wizard | Publishing wizard opens |
| 28 | Proceed to validation step and click "Validate" | AI validation runs |
| 29 | Verify validation result shows WARN status (not FAIL) | Validation status is "WARN" or equivalent warning indicator |
| 30 | Verify warning message indicates "generic name" or suggests a more descriptive name | Warning message describes the generic name issue |
| 31 | Verify "Publish" or "Next" button is ENABLED (publishing is allowed despite warning) | Publish button is enabled |
| 32 | Click Publish or proceed to publish | Publishing proceeds successfully |
| 33 | Verify skill is published and appears in catalog (if applicable) | Skill is published despite the warning |

### Part 5: WARN Status Allows Publishing — Missing Icon

| # | Action | Expected Result |
|---|--------|-----------------|
| 34 | Create a new skill with Name "Well Described Skill" (descriptive name) | Skill is created successfully |
| 35 | Enter Instructions: "This skill provides comprehensive assistance with data analysis tasks." (quality content) | Instructions are complete |
| 36 | Do NOT upload a custom icon (leave default icon) | Skill uses default icon |
| 37 | Save the skill and navigate to Publishing wizard | Publishing wizard opens |
| 38 | Proceed to validation step and click "Validate" | AI validation runs |
| 39 | Verify validation result shows WARN status | Validation status is "WARN" |
| 40 | Verify warning message indicates "no custom icon" or suggests adding one | Warning message describes missing icon |
| 41 | Verify "Publish" button is ENABLED | Publish button is enabled |
| 42 | Click Publish | Publishing proceeds successfully |
| 43 | Verify skill is published with default icon | Skill is published with warnings acknowledged |

---

## Expected Final State

- Skills with FAIL-status issues (short content, placeholders, secrets) cannot be published
- Validation error messages clearly describe the blocking issues
- Skills with WARN-status issues (generic name, missing icon) CAN be published
- Warning messages clearly describe the non-blocking issues
- Publish button is disabled for FAIL status and enabled for WARN status
- Skills with warnings are successfully published when user proceeds

---

## Pass/Fail Criteria

**Pass:**
- Short content skill validation returns FAIL status and blocks publishing
- Placeholder content skill validation returns FAIL status and blocks publishing
- Secret-containing skill validation returns FAIL status and blocks publishing
- Generic name skill validation returns WARN status and allows publishing
- Missing icon skill validation returns WARN status and allows publishing
- All error/warning messages are clear and describe the specific issue
- Publish button state correctly reflects blocker vs. warning status

**Fail:**
- Any FAIL-status skill is allowed to publish
- Any WARN-status skill is blocked from publishing
- Validation does not detect short content, placeholders, or secrets
- Error/warning messages are missing or unclear
- Publish button is enabled for FAIL status or disabled for WARN status
- Any step produces an error or unexpected result

---

## Notes

**Source functional tests:** ELITEA-2596, ELITEA-2598

**Regression rationale:** Consolidated from 2 tests covering AI validation scenarios with different outcomes: (1) ELITEA-2596 tests FAIL blockers that prevent publishing (short content, placeholders, secrets), and (2) ELITEA-2598 tests WARN scenarios that allow publishing (generic name, missing icon). These tests cover the same validation feature but with different severity levels and can be merged into a single comprehensive validation test.

**Selected checkpoints:**
- Short content → FAIL → publish blocked
- Placeholder → FAIL → publish blocked
- Secret detected → FAIL → publish blocked
- Generic name → WARN → publish allowed
- Missing icon → WARN → publish allowed
- All validation messages are clear and specific
