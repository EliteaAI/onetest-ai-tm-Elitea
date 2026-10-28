---
id: ELITEA-1995
title: "Build with AI — instructions character limit is enforced"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1995: Build with AI — instructions character limit is enforced

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Instructions field in the Build with AI review form enforces the platform's configured Skill instructions limit (default 50000 characters), blocking further input at the cap and disabling "Create Skill" only when genuinely invalid, per EliteaAI/elitea_issues#6744.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- A skill draft has been generated and the review/edit form is displayed.
- Platform is at the default "Skill Content Max Length" of 50000 characters.

> **Note:** This limit is admin-configurable via Admin → Settings → Runtime ("Skill Content Max Length"). This test case validates behavior against the default value (50000) only; changing the setting itself is out of scope here.

---

## Test Data

| Field | Value |
|-------|-------|
| Exact-limit instructions | A string of exactly 50000 characters |
| Over-limit paste | A string of 50001+ characters pasted in one paste |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate a skill draft and enter the review form | The review/edit form is displayed |
| 2 | Clear the Instructions field and type or paste text past 50000 characters | Input is hard-blocked at exactly 50000 characters; no further characters can be typed or pasted |
| 3 | Paste a block of text that would take the field from under the limit to over 50000 characters in one paste | Pasted text is truncated to land exactly at 50000 characters; no error shown, no crash |
| 4 | With the Instructions field at exactly 50000 characters, verify the "Create Skill" button | "Create Skill" remains enabled |
| 5 | Verify no hardcoded "2500" character limit message or counter appears anywhere in the form | Only the configured limit (50000 by default) is referenced |

---

## Expected Final State

The Instructions field follows the platform's configured Skill instructions limit (50000 by default), with the same hard-input-block behavior as the main Skill editor; "Create Skill" stays enabled as long as content is at or under the limit.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Input is hard-blocked at exactly 50000 characters, with no stale 2500-character limit or message anywhere in the form.

**Fail:**
- The form still enforces a 2500-character limit, or allows typing/pasting past 50000 characters, or blocks "Create Skill" at exactly 50000 characters.
