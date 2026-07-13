---
id: ELITEA-1871
title: "Create agent — instructions field alone does not enable Save (name+description both required)"
priority: high
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1871: Create agent — instructions field alone does not enable Save (name+description both required)

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that the Save button on the Create Agent form only becomes enabled when both the Name and Description fields are filled, and that filling only one field or only Instructions is insufficient.

---

## Preconditions

- User is logged in to the Elitea platform.
- The Create Agent page is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Instructions text | Any test instructions text |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Create Agent page | The Create Agent form is displayed with all fields empty |
| 2 | Leave Name and Description empty, fill only the Instructions field | Instructions field accepts input |
| 3 | Verify the Save button is disabled | Save button remains disabled |
| 4 | Fill Name only — verify Save is still disabled | Name field is filled; Save button remains disabled |
| 5 | Clear Name, fill Description only — verify Save is still disabled | Description field is filled; Save button remains disabled |
| 6 | Fill both Name and Description — verify Save becomes enabled | Save button becomes enabled (clickable) |

---

## Expected Final State

With both Name and Description filled, the Save button is enabled. Filling only one or neither required field keeps it disabled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Save button enables only when both Name and Description are filled.

**Fail:**
- Any step produces an error or unexpected result.
- Save button becomes enabled with only one required field filled, or remains disabled even with both filled.
