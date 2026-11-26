---
id: ELITEA-4966
title: "Compare skill versions: header Save stores the Instructions and file edits to one version; blank Instructions and unsaved changes are guarded"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [feat:skills, nfr:ui, nfr:usability, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7675]
---

# ELITEA-4966: Compare skill versions: header Save stores the Instructions and file edits to one version; blank Instructions and unsaved changes are guarded

**Module:** skills · **Priority:** critical · **Type:** regression

**Objective:** Verify that the single Save in each skill version header stores the Instructions and text file edits of that version only, that blank Instructions block saving, and that the discard warning protects unsaved edits on ← Select versions.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill `regression-compare-files` has draft versions `base` and `v2` (the same skill and files as ELITEA-4965).
- Before each run, the Instructions of base and v2 and `references/guide.md` in v2 do not contain `REG-INSTR` or `REG-FILE`.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Instructions marker | `REG-INSTR` |
| File marker | `REG-FILE` |
| File | `references/guide.md` |
| Blank Instructions tooltip | `Instructions cannot be empty.` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `regression-compare-files` → ⋮ → **Compare versions**, Base = `base`, Compare with = `v2`, click **Compare** | Each version header has one **Save** on the right, disabled. There is no Save under the fields |
| 2 | Append ` REG-INSTR` to the V2 Instructions | V2 **Save** is enabled. BASE **Save** stays disabled |
| 3 | Click **Next**, select `references/guide.md` and append ` REG-FILE` in the V2 column | V2 **Save** is still enabled |
| 4 | Click **Save** in the V2 header | Toast `Version "v2" has been updated.` appears. V2 **Save** becomes disabled |
| 5 | Click **Previous**, clear the BASE Instructions and hover BASE **Save** | BASE **Save** is disabled with the tooltip `Instructions cannot be empty.` |
| 6 | Click **← Select versions** | The warning `Discard unsaved changes?` appears |
| 7 | Confirm discard, then click **Compare** again with the same versions | The BASE Instructions show their saved text (not blank) |
| 8 | Close the modal. Select version `v2` on the skill page and check the Instructions and the Files tab | The Instructions contain `REG-INSTR`. `references/guide.md` contains `REG-FILE` |
| 9 | Select version `base` and check the same places | Neither marker is present |
| 10 | Cleanup: remove ` REG-INSTR` and ` REG-FILE` from v2 and save | v2 is back to the test data |

---

## Expected Final State

Both versions match the test data again after cleanup; during the run only v2 held both edits.

---

## Pass/Fail Criteria

**Pass:**
- One header Save stores the Instructions and file edits to its own version only.
- Blank Instructions block saving, with the tooltip.
- The discard warning appears on ← Select versions with unsaved edits.

**Fail:**
- An edit is lost or saved to the wrong version.
- A version is saved with blank Instructions.
- No warning appears on ← Select versions.

---

## Notes

**Source functional tests:** ELITEA-4961, ELITEA-4962
**Regression rationale:** The header Save is new and writes the Instructions and several files at once, so it is the riskiest data path of EliteaAI/elitea_issues#7675.
**Selected checkpoints:** header Save state per version; save of Instructions and file together; isolation between versions; blank-Instructions tooltip; discard warning.
**Not covered:** partial save failure, line endings and byte order mark preservation, the published version, the Viewer role (see the functional cases).
