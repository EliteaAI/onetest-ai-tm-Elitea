---
id: ELITEA-2613
title: "Edit with AI — Skill Permissions"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, feat:edit-with-ai, feat:permissions]
requirements: []
---

# ELITEA-2613: Edit with AI — Skill Permissions

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that "Edit with AI" CTA is visible for Admin and Editor roles but hidden for Viewer role, and optionally verify character limit enforcement for instructions (the platform's configured Skill instructions limit, default 50,000 characters, per EliteaAI/elitea_issues#6744).

---

## Preconditions

- User accounts exist with different roles:
  - Admin role user
  - Editor role user
  - Viewer role user
- A project exists and is accessible to all test users.
- The Skills section is available in the project.
- An existing skill exists that can be viewed/edited.

> **Note:** The instructions character limit (Part D) is admin-configurable via Admin → Settings → Runtime ("Skill Content Max Length"). Part D validates behavior against the default value (50,000) only; changing the setting itself is out of scope here.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill Name | `permission-test-skill` |
| Admin User | User with Admin role in the project |
| Editor User | User with Editor role in the project |
| Viewer User | User with Viewer (read-only) role in the project |
| Long Instructions | Text exceeding the configured Skill instructions limit (50,000 characters by default) |

---

## Steps

### Part A: Admin Role — CTA Visible

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as Admin user | Login successful |
| 2 | Navigate to the project and Skills section | Skills list loads |
| 3 | Open the test skill's detail page | Skill detail page loads |
| 4 | Verify "Edit with AI" CTA/button is visible | Button is present and enabled |
| 5 | Click "Edit with AI" | Wizard opens successfully |
| 6 | Close the wizard | Wizard closes |

### Part B: Editor Role — CTA Visible

| # | Action | Expected Result |
|---|--------|-----------------|
| 7 | Log out and log in as Editor user | Login successful |
| 8 | Navigate to the same project and skill | Skill detail page loads |
| 9 | Verify "Edit with AI" CTA/button is visible | Button is present and enabled |
| 10 | Click "Edit with AI" | Wizard opens successfully |
| 11 | Close the wizard | Wizard closes |

### Part C: Viewer Role — CTA Hidden

| # | Action | Expected Result |
|---|--------|-----------------|
| 12 | Log out and log in as Viewer user | Login successful |
| 13 | Navigate to the same project and skill | Skill detail page loads (read-only mode) |
| 14 | Verify "Edit with AI" CTA/button is NOT visible | Button is hidden or absent |
| 15 | Verify no edit capabilities are available | Page is in view-only mode |

### Part D: (Optional) Character Limit Enforcement

| # | Action | Expected Result |
|---|--------|-----------------|
| 16 | Log in as Admin or Editor | Login successful |
| 17 | Open "Edit with AI" for a skill | Wizard opens |
| 18 | Generate suggestions | Suggestions displayed |
| 19 | Manually edit the "Suggested" instructions field | Field is editable |
| 20 | Attempt to type or paste text past the configured limit (50,000 characters by default) | Input is hard-blocked at exactly the configured limit; no further characters can be typed or pasted, no error message shown |
| 21 | Paste a block of text that would take the field from under the limit to over the limit in one paste | Pasted text is truncated to land exactly at the configured limit; no error shown, no crash |
| 22 | Verify Apply/Save remains enabled with content at exactly the configured limit | Apply/Save is not blocked when content is at or under the limit |

---

## Expected Final State

1. Admin users see "Edit with AI" CTA and can use the feature.
2. Editor users see "Edit with AI" CTA and can use the feature.
3. Viewer users do NOT see "Edit with AI" CTA (feature hidden).
4. (Optional) Instructions field follows the platform's configured Skill instructions limit (50,000 characters by default), with no stale 2,500-character limit remaining anywhere in the form.

---

## Pass/Fail Criteria

**Pass:**
- Admin can see and use "Edit with AI".
- Editor can see and use "Edit with AI".
- Viewer cannot see "Edit with AI" CTA.
- Character limit (if tested) follows the configured limit, not a stale 2,500-character limit.

**Fail:**
- Admin or Editor cannot access "Edit with AI".
- Viewer can see "Edit with AI" CTA.
- Character limit (if tested) is still capped at 2,500 characters, or allows typing/pasting past the configured limit.
