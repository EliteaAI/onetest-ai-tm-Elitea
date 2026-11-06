---
id: ELITEA-4354
title: "Regression: normal Excel workbooks index all sheets and rows, with default and token-based chunking"
priority: high
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, int:artifact-toolkit, issue:7286, excel, regression, p1]
requirements: ["EliteaAI/elitea_issues#7286"]
---

# ELITEA-4354: Regression: normal Excel workbooks index all sheets and rows, with default and token-based chunking

**Module:** indexing · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify that workbooks with no whole-column ranges index exactly as before the #7286 fix: every sheet and every row is indexed, sparse sheets keep their empty rows between data, and token-based chunking splits large sheets into several chunks.

---

## Preconditions

- A user with access to project **P**, logged in to `{{base_url}}`.
- An Artifact toolkit **T** in P with an empty bucket **B**.
- The embedding model for P is configured.

---

## Test Data

| File | Content |
|---|---|
| `orders_table.xlsx` | Sheet **Orders**: header `order | customer | amount` and 200 rows for orders 1–200. Customer is `customer N`, where N = order mod 17, and amount = order × 1.5. For example: `150 | customer 14 | 225` and `200 | customer 13 | 300`. In Excel: A2 `1`, B2 `="customer "&MOD(A2,17)`, C2 `=A2*1.5`, filled down to row 201, then copied and pasted as values. |
| `sparse_two_sheets.xlsx` | Sheet **Sparse**: `top` in A1, `middle` in C3 with a cell comment, `bottom` in B6, and nothing else. Sheet **Second**: one row `only | row`. |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload both files to bucket B. Create an index with the suffix `xlrange5` and default chunking settings, and run it. | Indexing completes. Both files are listed as indexed in **History**. |
| 2 | Search for `customer 14`. | Results come from the **Orders** sheet of `orders_table.xlsx`. |
| 3 | Search for `200`. | The last order row (`200 | customer 13 | 300`) is in the indexed text, so no row was lost at the end. |
| 4 | Search for `bottom`. | The **Sparse** chunk is returned. It has 6 lines: `top`, an empty row, `middle` on row 3, two empty rows, and `bottom` on row 6. The sheet ends at row 6. |
| 5 | Search for `only row`. | The **Second** sheet chunk is returned. |
| 6 | Create a second index with the suffix `xlrange6`. In the chunking settings for Excel, set **max_tokens** to `50`. Run it. | Indexing completes. |
| 7 | In **History** for `xlrange6`, check the chunk count for `orders_table.xlsx`. | `orders_table.xlsx` is split into many chunks (about 40), not 1. |
| 8 | Search `xlrange6` for `customer 14`. | Several results are returned, each a small part of the **Orders** table. |

---

## Expected Final State

Both normal workbooks are fully indexed under both chunking settings, with no rows lost and no rows added.

---

## Pass/Fail Criteria

**Pass:**
- All rows on all sheets are searchable in both indexes.
- The **Sparse** sheet keeps its gaps between data and ends at row 6.
- With `max_tokens = 50`, `orders_table.xlsx` is split into many chunks.

**Fail:**
- A sheet or row is missing from the index.
- Empty rows are added after the last data row, or the gaps in **Sparse** disappear.
- `max_tokens` has no effect on the number of chunks.
