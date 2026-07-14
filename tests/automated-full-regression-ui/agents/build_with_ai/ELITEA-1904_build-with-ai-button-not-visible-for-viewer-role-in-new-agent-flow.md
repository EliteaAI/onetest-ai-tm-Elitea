---
id: ELITEA-1904
title: "Build with AI — Build with AI button is NOT visible for viewer role in New Agent flow"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1904: Build with AI — Build with AI button is NOT visible for viewer role in New Agent flow

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that users with a viewer role cannot see the Magic Wand (Build with AI) button on the New Agent creation page, ensuring the AI Agent Creator flow is properly restricted by role-based access control.

---

## Preconditions

- User is logged in to the Elitea platform.
- A user with viewer role exists in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Viewer user credentials | Valid viewer role account |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as a user with viewer role | Viewer user is logged in successfully |
| 2 | Navigate to Agents and attempt to open the New Agent creation page | The New Agent creation page opens (if accessible) or navigation is restricted |
| 3 | Verify the Magic Wand button is NOT displayed anywhere on the creation page | The Magic Wand (Build with AI) button is absent from the creation page |
| 4 | Verify there is no way for a viewer to trigger the AI Agent Creator flow | No UI control exists that would allow the viewer to initiate the Build with AI flow |

---

## Expected Final State

The Magic Wand (Build with AI) button is not visible or accessible to viewer role users on the New Agent creation page.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The Build with AI button is not present for the viewer role at any point in the New Agent creation flow.

**Fail:**
- Any step produces an error or unexpected result.
- The Build with AI button is visible or accessible to the viewer role user.
