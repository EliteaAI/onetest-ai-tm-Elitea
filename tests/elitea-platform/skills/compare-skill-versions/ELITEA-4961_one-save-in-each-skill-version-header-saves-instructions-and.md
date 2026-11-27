---
id: ELITEA-4961
title: "One Save in each skill version header saves Instructions and file edits to that version only"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, nfr:ui, nfr:usability, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7675]
---

# ELITEA-4961: One Save in each skill version header saves Instructions and file edits to that version only

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify the header Save that replaces per-field Save for skills: edits on Instructions and text files are saved together to the correct version, blank Instructions block saving, a failed file is reported by name, and CRLF / BOM are preserved.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill **Compare Files QA** has draft versions `base` and `v2`; their files are uploaded from `test-data/EL-7675/compare-files-qa/base/` and `compare-files-qa/v2/` (see the README there for the expected chips).

---

## Test Data

| Field | Value |
|-------|-------|
| Skill | Compare Files QA |
| Text file | `references/guide.md`, `scripts/run.py` |
| CRLF + BOM file | `references/crlf.md` (base: `EF BB BF`, CRLF) |
| Edit markers | `INSTR-EDIT`, `FILE-A` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open skill **Compare Files QA** → actions menu (⋮) → **Compare versions**, Base = `base`, Compare with = `v2`, click **Compare**. | Each version header: name, date · author, and one **Save** on the right (disabled); no Save under the fields. |
| 2 | Append ` INSTR-EDIT` to the V2 Instructions; **Next**; open `references/guide.md`. | Red/green word highlights per side; Copy icon above each column; V2 Save enabled, BASE Save disabled. |
| 3 | Append ` FILE-A` to V2 guide.md and click **Save** in the V2 header. | Toast `Version "v2" has been updated.`; V2 Save disabled. |
| 4 | In BASE `references/crlf.md` change `alpha` to `beta`; click BASE **Save**. | Toast for base. |
| 5 | Go **Previous**, clear the V2 Instructions; hover the V2 Save. | Save disabled, tooltip `Instructions cannot be empty.`; it stays disabled after editing a V2 file on the Files step. |
| 6 | Restore V2 Instructions. In DevTools block the save request for `scripts/run.py`, edit V2 run.py and click V2 **Save**. | Error toast `scripts/run.py was not saved: …`; Instructions saved; run.py edit stays pending. |
| 7 | Unblock and click V2 **Save** again. | Success toast. |
| 8 | Close the modal; check v2 and base on the skill page Files tab; download base `crlf.md`. | v2 has `INSTR-EDIT`, `FILE-A` and the run.py edit; base guide.md unchanged; base crlf.md still starts with `EF BB BF` and uses CRLF, only `beta` changed. |

---

## Expected Final State

v2 holds all its edits; base holds only the crlf.md edit.

---

## Pass/Fail Criteria

**Pass:**
- Header Save persists all pending edits of its version only.
- Blank Instructions and partial failures are handled as designed; line endings and BOM kept.

**Fail:**
- Edit saved to the wrong version or lost.
- Version saved with blank Instructions.
- Generic error without the file name.
- BOM removed or CRLF converted.
