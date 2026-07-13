---
id: ELITEA-1898
title: "Copy version link produces a version-specific URL"
priority: medium
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1898: Copy version link produces a version-specific URL

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that the "Copy Link" button produces a version-specific URL (containing the version ID), and that navigating to the copied URL opens the correct agent at the correct version.

---

## Preconditions

- User is logged in to the Elitea platform.
- An agent with at least one named version is available.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page and select a specific named version | The named version is active |
| 2 | Locate the "Copy Link" button in the toolbar or three-dot menu | The Copy Link button is visible |
| 3 | Click it — verify a visual confirmation appears (e.g., "Copied!" tooltip or icon change) | A visual confirmation (tooltip or icon change) is displayed |
| 4 | Paste the copied URL and inspect it | The URL is available for inspection |
| 5 | Verify the URL contains the version ID (not just the agent URL) | The URL includes the version identifier |
| 6 | Navigate to the copied URL — verify it opens the correct agent at the correct version | The agent opens at the expected version |

---

## Expected Final State

The copied URL contains the version ID and, when navigated to, opens the correct agent at the correct version.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The copied URL is version-specific and opens the correct agent version when navigated.

**Fail:**
- Any step produces an error or unexpected result.
- The copied URL is a generic agent URL without the version ID, or navigating to it opens the wrong version.
