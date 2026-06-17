---
id: ELITEA-0373
title: "DOCX Structured Content Rendered and Preserved [lists / tables / images / headers / footers / page breaks]"
priority: high
type: functional
module: canvas
status: draft
execution_type: manual
tags: [feat:canvas, story:3648]
requirements: [ProjectAlita/projectalita.github.io#3648]
---
# ELITEA-0373: DOCX Structured Content Rendered and Preserved [lists / tables / images / headers / footers / page breaks]

**Module:** Canvas · **Priority:** High · **Type:** Functional

**Objective:** Verify that structured content types in a DOCX (lists, tables, images, headers/footers, page breaks) are rendered in SuperDoc and preserved after editing and saving.

**Coverage (parametrized by content type):**
- Bulleted list: rendered, editable, and preserved after save
- Numbered list: rendered, editable, and preserved after save
- Table: rendered and cell content editable
- Embedded images: rendered/displayed in the editor
- Headers and footers: visible in the editor
- Page breaks: visible and preserved

## Preconditions

- Logged in to {{base_url}}
- Test file `structured-content.docx` uploaded to bucket `test-docx-bucket`
- File contains: bulleted list, numbered list, 2×2 table, 1 embedded image, header text "Test Header", footer text "Page 1", one manual page break

## Test Data

- File: `structured-content.docx` in bucket `test-docx-bucket`
- Edit: change one bulleted list item to `"BULLET_EDIT"`, one numbered list item to `"NUMBER_EDIT"`, one table cell to `"CELL_EDIT"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open `structured-content.docx` in Canvas from Artifacts | SuperDoc loads; bulleted list, numbered list, table, embedded image, header, footer, and page break are all visually present |
| 2 | Edit one item in the bulleted list to `BULLET_EDIT` and one in the numbered list to `NUMBER_EDIT` | Changes are reflected in the editor |
| 3 | Edit a cell in the table to `CELL_EDIT` | Cell content is updated in the editor |
| 4 | Click Save | Save succeeds; success notification appears |
| 5 | Close and reopen the file from Artifacts | Edited list items and table cell show the new values; image, header, footer, and page break are still present and intact |

## Expected Final State

Edited list items and table cell show the new values; image, header, footer, and page break are still present and intact

## Pass/Fail Criteria

**Pass:**
- All 6 content types render on open
- Edited list items and table cell are preserved after save/reopen
- Non-edited structured elements (image, header, footer, page break) remain intact

**Fail:**
- Any content type is missing on open
- Any edited value is lost after save/reopen
- Structured elements are corrupted or cause an editor crash
