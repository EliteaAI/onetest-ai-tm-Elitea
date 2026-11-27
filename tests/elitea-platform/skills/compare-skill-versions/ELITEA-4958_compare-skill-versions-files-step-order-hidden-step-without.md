---
id: ELITEA-4958
title: "Compare skill versions: Files step order, hidden step without files and bottom bar navigation"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, nfr:ui, nfr:usability, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7675]
---

# ELITEA-4958: Compare skill versions: Files step order, hidden step without files and bottom bar navigation

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify the three-step flow (Instructions → Files → Run settings), that the Files step is hidden when neither version has files, and the new bottom bar (← Select versions on the left; Next / Previous / Finish on the right).

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill **Compare Files QA** has draft versions `base` and `v2`; their files are uploaded from `test-data/EL-7675/compare-files-qa/base/` and `compare-files-qa/v2/` (see the README there for the expected chips).
- Skill **Compare No Files QA** has 2 versions without files (`compare-no-files-qa/`).
- Skill **Compare One Side Files QA**: base has no files, v2 has `references/a.md` (`compare-one-side-files-qa/`).

---

## Test Data

| Field | Value |
|-------|-------|
| Skills | Compare Files QA, Compare No Files QA, Compare One Side Files QA |
| Test data | `test-data/EL-7675/` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open skill **Compare Files QA** → actions menu (⋮) → **Compare versions**, Base = `base`, Compare with = `v2`, click **Compare**. | Modal opens on **1. Instructions**; three step bars; bottom bar: **← Select versions** on the left, only **Next** on the right. |
| 2 | Append ` STEP-EDIT` to the V2 Instructions, click **Next**. | **2. Files** opens with the file tree and BASE / V2 columns; right side shows **Previous** and **Next**. |
| 3 | Click **Next**. | **3. Run settings** shows the run settings diff; right side shows **Previous** and **Finish**; no Save in the version headers. |
| 4 | Click **Previous** twice. | Instructions step still shows the unsaved ` STEP-EDIT`. |
| 5 | Click **← Select versions** and confirm **Discard** in the warning. | `Discard unsaved changes?` appears; after Discard the version selection opens. |
| 6 | Compare the versions of **Compare No Files QA**. | Two step bars: Instructions, then Run settings as step 2 with **Previous** and **Finish**; no Files step. |
| 7 | Compare the versions of **Compare One Side Files QA** and click **Next**. | Files step is shown; `references/a.md` has the **New** chip. |
| 8 | On the last step click **Finish**. | Modal closes. |

---

## Expected Final State

No version data changed.

---

## Pass/Fail Criteria

**Pass:**
- Steps are in order and the Files step appears only when a version has files.
- Bottom bar buttons match each step; edits survive step navigation.

**Fail:**
- Files step missing, empty or out of order.
- Wrong buttons on a step or edits lost when switching steps.
