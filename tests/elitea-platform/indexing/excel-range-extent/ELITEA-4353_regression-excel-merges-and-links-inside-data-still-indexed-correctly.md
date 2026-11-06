---
id: ELITEA-4353
title: "Regression: merged cells and hyperlinks inside the data of an Excel sheet are still indexed correctly"
priority: high
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, int:artifact-toolkit, issue:7286, excel, regression, p1]
requirements: ["EliteaAI/elitea_issues#7286"]
---

# ELITEA-4353: Regression: merged cells and hyperlinks inside the data of an Excel sheet are still indexed correctly

**Module:** indexing · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that the #7286 fix, which cuts merge and hyperlink ranges off at the last data row, does not change how normal merges and links inside the data are indexed. Link text and URLs must stay in the indexed text, and the value of a merged cell must appear once, at its top-left cell.

---

## Preconditions

- A user with access to project **P**, logged in to `{{base_url}}`.
- An Artifact toolkit **T** in P with an empty bucket **B**.
- The embedding model for P is configured.

---

## Test Data

Create `report_inside_ranges.xlsx` with one sheet **Report**:

| Row | A | B | C |
|---|---|---|---|
| 1 | `Quarterly report` (merged A1:C1) | | |
| 2 | `site` | `link` | `note` |
| 3 | `Docs` | `docs` → link to `https://example.com/docs` | `x` |
| 4 | `Wiki` | `wiki` → link to `https://example.com/wiki` | |
| 5 | `Group` (merged A5:A6) | | `merged` |
| 6 | | `under merge` | |
| 7 | `Jump` | `to Orders` → link to a cell in this workbook | |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `report_inside_ranges.xlsx` to bucket B. Create an index with the suffix `xlrange4` and default chunking settings, and run it. | Indexing completes within about 1 minute. |
| 2 | Search for `Quarterly report`. | The **Report** chunk is returned. `Quarterly report` appears once, on the first line. |
| 3 | Search for `example.com/docs`. | The chunk is returned, and the row reads `Docs | [docs](https://example.com/docs) | x`, with both the link text and the URL. |
| 4 | Search for `wiki`. | The row `Wiki | [wiki](https://example.com/wiki) |` is in the chunk. |
| 5 | Search for `under merge`. | The chunk is returned. `Group` appears once (on row 5), and `under merge` is on row 6. |
| 6 | Check the full text of the chunk from step 2. | The chunk has exactly 7 lines, one per row. No empty lines are added after row 7. |

---

## Expected Final State

The **Report** sheet is indexed as 7 lines, with link text and URLs kept and merged values shown once.

---

## Pass/Fail Criteria

**Pass:**
- Steps 2–6 all match the expected text.

**Fail:**
- A link's URL or text is missing, or a merged value is repeated on several rows.
- Rows are missing, or empty rows are added after the data.
