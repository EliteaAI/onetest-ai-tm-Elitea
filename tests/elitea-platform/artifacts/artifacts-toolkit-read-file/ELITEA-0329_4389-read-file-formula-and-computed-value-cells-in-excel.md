---
id: ELITEA-0329
title: "[EliteaAI/elitea_issues#4389] read_file — Formula and Computed-Value Cells in Excel"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, issue:4389, read_file, edge-case, r-2.0.3, excel]
requirements: [4389]
---
# ELITEA-0329: [EliteaAI/elitea_issues#4389] read_file — Formula and Computed-Value Cells in Excel

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `read_file` handles formula cells in Excel files consistently — returning either the calculated/displayed values or the raw formula strings — and that the behavior is stable and predictable across calls.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured via Toolkit Test Settings.
`formulas.xlsx` is uploaded to an artifact bucket.
Sheet \"Calc\" contains:
- Column A: raw numbers (10, 20, 30)
- Column B: SUM formula (=SUM(A1:A3) → 60)
- Column C: concatenation formula (=\"Hello \"&A1 → \"Hello 10\")
- Column D: static text (\"Static\")
The file was saved with calculated values cached (standard Excel save).

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file` with `sheet_name`: "Calc". | Response returns values for all columns. Column B returns either the calculated value (60) OR the formula string (=SUM(A1:A3)) — not a blank or error. Column C returns either "Hello 10" OR the formula string — not blank. Column D returns "Static" as plain text. Behavior is consistent (all formulas return values, or all return formula strings — not a mix). |
| 2 | Call `read_file` with `sheet_name`: "Calc" a second time (identical call). | Output is identical to step 1. Results are stable and deterministic across repeated calls. |

## Expected Final State

Output is identical to step 1. Results are stable and deterministic across repeated calls.

## Pass/Fail Criteria

PASS: Formula cells return non-blank values consistently; same result on repeated calls; no crash.
FAIL: Formula cells return blank; crash on formula cell; inconsistent values between calls (e.g., sometimes value, sometimes formula string).
