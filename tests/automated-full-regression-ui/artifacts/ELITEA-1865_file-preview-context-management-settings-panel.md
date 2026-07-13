---
id: ELITEA-1865
title: "File Preview/Edit – Context Management Settings Panel Opens for Supported File"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1865: File Preview/Edit – Context Management Settings Panel Opens for Supported File

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that opening a supported file in the "afa" bucket displays a Context Management settings panel with all required configuration fields and functional Cancel/Save buttons.

---

## Preconditions

- User is logged in to the Elitea platform.
- The "afa" bucket exists and contains "1.png".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | afa |
| File name | 1.png |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section and click on the "afa" bucket in the bucket list | "afa" bucket is selected |
| 2 | Verify the left panel tree shows the "afa" bucket with files including "1.png" | "1.png" is visible |
| 3 | Hover over "1.png" and click the "View/Edit file" icon | File opens and Context Management panel appears |
| 4 | Verify the file opens and a "Context Management" settings panel appears | Context Management panel is visible |
| 5 | Verify the panel contains: toggle/switch control, "Context Window" and "Max Tokens" fields | Required fields are present |
| 6 | Verify a "Content Strategy & Token Management" section with "Context First", "Context Tokens", "Preserve Recent Messages", "Summarized Link Count" fields | All content strategy fields are present |
| 7 | Verify a "Summarization" section with an "Enable automatic summarization" toggle | Toggle is present |
| 8 | Verify "Summarization Instructions" text area is present | Text area is visible |
| 9 | Verify "Summary Model", "Summary Trigger Ratio", "Attribute: Clause & Format", "Target Summary Tokens" fields are present with values | All summarization fields are present |
| 10 | Verify an "External Messages" section with "Always preserve system messages" toggle | Toggle is present |
| 11 | Verify "Custom Instructions" text area with placeholder "You are a helpful assistant." | Text area with placeholder is visible |
| 12 | Verify "Cancel" and "Save" buttons are at the bottom | Both buttons are present |
| 13 | Verify the "Cancel" button closes the panel without saving | Cancel closes the panel |
| 14 | Verify the "Save" button saves the context management settings | Save operation completes successfully |

---

## Expected Final State

The Context Management settings panel is displayed for the "afa" bucket file with all required fields and functional Cancel/Save buttons.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Context Management panel displays all required fields; Cancel and Save work correctly.

**Fail:**
- Any step produces an error or unexpected result.
- Context Management panel missing, required fields absent, or buttons non-functional.
