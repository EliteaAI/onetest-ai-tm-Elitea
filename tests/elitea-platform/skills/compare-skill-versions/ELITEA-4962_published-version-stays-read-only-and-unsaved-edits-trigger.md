---
id: ELITEA-4962
title: "Published version stays read-only and unsaved edits trigger the discard warning in skill compare"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, nfr:ui, nfr:usability, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7675]
---

# ELITEA-4962: Published version stays read-only and unsaved edits trigger the discard warning in skill compare

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that a published version cannot be edited on the Instructions or Files steps, and that unsaved edits are protected on ← Select versions and on close.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill **Compare Files QA** has draft versions `base` and `v2`; their files are uploaded from `test-data/EL-7675/compare-files-qa/base/` and `compare-files-qa/v2/` (see the README there for the expected chips).
- Version `v-published` of Compare Files QA has the files of `compare-files-qa/v-published/` and is published.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill | Compare Files QA |
| Published version | v-published |
| Edit marker | `UNSAVED` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Compare Base = `v-published`, Compare with = `v2`. | Instructions of v-published are read-only; its header has no enabled Save. |
| 2 | **Next**; select `references/guide.md` and try to type in the v-published column. | Text cannot be changed; v-published Save stays disabled; V2 column is editable. |
| 3 | Append ` UNSAVED` in V2 guide.md, click **← Select versions**. | Warning `Discard unsaved changes?` appears. |
| 4 | Cancel. | Modal stays on Files with the edit kept. |
| 5 | Click ✕ (Close). | Unsaved changes warning appears. |
| 6 | Confirm discard; reopen the comparison and open guide.md. | Text has no `UNSAVED`; v-published is unchanged. |
| 7 | Without editing, click **← Select versions**. | Version selection opens without a warning. |

---

## Expected Final State

No version data changed.

---

## Pass/Fail Criteria

**Pass:**
- Published side cannot be edited or saved.
- Warning appears only when there are unsaved edits.

**Fail:**
- Any change saved to the published version.
- Unsaved edits lost without a warning.
