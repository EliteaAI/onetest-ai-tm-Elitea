---
id: ELITEA-2438
title: "Import Skill with missing required frontmatter shows validation error"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-2438: Import Skill with missing required frontmatter shows validation error

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that Import Skill with missing required frontmatter shows validation error. Success is confirmed when verify no skill is created.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Prepare a .md file with missing required frontmatter (e.g., no `name` field) | Action completes without error and produces the expected UI state. |
| 2 | Attempt to import it via Skills → Import | Action completes without error and produces the expected UI state. |
| 3 | Verify the system shows a user-friendly validation error indicating the missing field | Condition holds as described. |
| 4 | Verify no Skill is created | Condition holds as described. |

---

## Expected Final State

Verify no Skill is created.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Import Skill with missing required frontmatter shows validation error.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
