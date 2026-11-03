---
id: ELITEA-4355
title: "Excel indexing time does not grow with the size of merge or hyperlink ranges that extend past the data [Parametrized]"
priority: medium
type: performance
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, int:artifact-toolkit, issue:7286, excel, p2]
requirements: ["EliteaAI/elitea_issues#7286"]
---

# ELITEA-4355: Excel indexing time does not grow with the size of merge or hyperlink ranges that extend past the data [Parametrized]

**Module:** indexing · **Priority:** Medium (P2) · **Type:** Performance

**Objective:** Verify that the time to index a small `.xlsx` file stays about the same whether its merge or hyperlink range ends at row 10,000, row 100,000 or the last row of the sheet. Before the fix, reading time and output size grew with the range size even though every file had the same 5 data rows.

---

## Preconditions

- A user with access to project **P**, logged in to `{{base_url}}`.
- An Artifact toolkit **T** in P with an empty bucket **B**.
- The embedding model for P is configured.
- The 7 test files below, all about 5 KB with the same 5 data rows on sheet **Data**. They can be generated with the `make_workbooks.py` script attached to EliteaAI/elitea_issues#7286.

---

## Test Data

| Variant | File | Range | Before the fix (read time / lines) |
|---|---|---|---|
| Control | `control_plain.xlsx` | none | 0.01 s / 5 |
| Merge 10k | `merge_10k_rows.xlsx` | merge `C1:C10000` | 0.25 s / 10,000 |
| Merge 100k | `merge_100k_rows.xlsx` | merge `C1:C100000` | 2.5 s / 100,000 |
| Merge whole column | `merge_whole_column.xlsx` | merge `C1:C1048576` | 23 s / 1,048,576 |
| Link 10k | `link_10k_rows.xlsx` | hyperlink `D1:D10000` | 0.39 s / 10,000 |
| Link 100k | `link_100k_rows.xlsx` | hyperlink `D1:D100000` | 6.1 s / 100,000 |
| Link whole column | `link_whole_column.xlsx` | hyperlink `D1:D1048576` | 47 s / 1,048,576 |

Times above cover reading the file only. The full index run before the fix also had to embed all of that text.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload all 7 files to bucket B. | All 7 files appear in the bucket, each about 5 KB. |
| 2 | Create an index with the suffix `xlperf_ctrl` that includes only `control_plain.xlsx` (set the include pattern to the file name). Run it and note the time from start to **Completed**. | Indexing completes. Note this time as the baseline. |
| 3 | Repeat step 2 for each of the other 6 files, with a new suffix each time (for example `xlperf_m10k`, `xlperf_m100k`, `xlperf_mall`, `xlperf_l10k`, `xlperf_l100k`, `xlperf_lall`). | Each run completes. |
| 4 | Compare the 7 times. | All times are close to the baseline from step 2, with the same order of magnitude. Bigger ranges do not take noticeably longer. |
| 5 | For each index, check the chunk count in **History**. | Every file has the same chunk count as the control file (1 with default settings). |

---

## Expected Final State

All 7 files index in about the same time and with the same number of chunks, whatever their range size.

---

## Pass/Fail Criteria

**Pass:**
- No run takes much longer than the control run, e.g. more than 3 times as long, or more than 1 minute.
- All files have the same chunk count.

**Fail:**
- Indexing time grows with the range size, especially for the whole-column files.
- Any run stays **In Progress** for many minutes, or ends **Stopped** / **Failed**.
