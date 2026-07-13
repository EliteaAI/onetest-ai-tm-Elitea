---
id: ELITEA-1903
title: "Build with AI — Build with AI button visible for admin and editor roles in New Agent creation flow"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1903: Build with AI — Build with AI button visible for admin and editor roles in New Agent creation flow

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that the Magic Wand (Build with AI) button is visible on the New Agent creation page for users with admin and editor roles, confirming that role-based access grants these roles access to the AI Agent Creator flow.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one project exists with users assigned as admin and editor roles respectively.
- The Build with AI feature is enabled.

---

## Test Data

| Field | Value |
|-------|-------|
| Admin user credentials | Valid admin role account |
| Editor user credentials | Valid editor role account |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as a user with admin role | Admin user is logged in successfully and the dashboard is displayed |
| 2 | Navigate to Agents and click "+ Create" to open the New Agent creation page | The New Agent creation page opens with the creation tab bar visible |
| 3 | Verify the Magic Wand (Build with AI) button is visible in the creation tab bar | The Magic Wand (Build with AI) button is present and visible in the tab bar |
| 4 | Log out and log in as a user with editor role | Editor user is logged in successfully |
| 5 | Navigate to Agents and click "+ Create" to open the New Agent creation page | The New Agent creation page opens with the creation tab bar visible |
| 6 | Verify the Magic Wand button is also visible for the editor role | The Magic Wand button is present and visible for the editor role |

---

## Expected Final State

The Magic Wand (Build with AI) button is visible in the New Agent creation tab bar for both admin and editor role users.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The Build with AI button is visible for both admin and editor roles on the New Agent creation page.

**Fail:**
- Any step produces an error or unexpected result.
- The Build with AI button is missing or hidden for admin or editor role users.
