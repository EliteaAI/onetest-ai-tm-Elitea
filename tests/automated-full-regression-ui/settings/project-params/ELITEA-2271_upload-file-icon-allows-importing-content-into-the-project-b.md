---
id: ELITEA-2271
title: "Upload file icon allows importing content into the Project Background editor"
priority: medium
type: functional
module: settings-project-params
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2271: Upload file icon allows importing content into the Project Background editor

**Module:** settings-project-params · **Priority:** medium · **Type:** functional

**Objective:** Verify that Upload file icon allows importing content into the Project Background editor. Success is confirmed when verify the imported content is editable.

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
| 1 | Navigate to Settings → Project Context | Target page/section loads successfully. |
| 2 | Click the upload file icon button next to the editor | Control responds; expected next state is shown. |
| 3 | Verify a file picker opens | Condition holds as described. |
| 4 | Select a supported text or markdown file | Control responds; expected next state is shown. |
| 5 | Verify the file contents are imported into the Project Background editor | Condition holds as described. |
| 6 | Verify the imported content is editable | Condition holds as described. |

---

## Expected Final State

Verify the imported content is editable.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Upload file icon allows importing content into the Project Background editor.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
