---
id: ELITEA-1878
title: "Add and save multiple tags — both persist after reload"
priority: medium
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1878: Add and save multiple tags — both persist after reload

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that multiple tags added to an agent are saved correctly and both tags persist after a page reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Tag 1 | regression-test |
| Tag 2 | automation |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page | The agent detail page loads |
| 2 | Add tag "regression-test" and tag "automation" | Both tags appear as chips in the Tags field |
| 3 | Click Save | Save completes successfully |
| 4 | Reload the page | The page reloads |
| 5 | Verify both "regression-test" and "automation" tags are shown in the Tags field | Both tag chips are displayed in the Tags field |

---

## Expected Final State

After reload, both "regression-test" and "automation" tags are present in the Tags field.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Both tags persist in the Tags field after page reload.

**Fail:**
- Any step produces an error or unexpected result.
- One or both tags are missing after reload.
