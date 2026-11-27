---
id: ELITEA-4960
title: "Binary and over-limit files are shown as cards with size and Download and cannot be edited"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, nfr:ui, nfr:usability, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7675]
---

# ELITEA-4960: Binary and over-limit files are shown as cards with size and Download and cannot be edited

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that files not compared as text (binary, or text over 50,000 characters) render as cards with name, size and Download, framed in orange only when the versions differ.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill **Compare Files QA** has draft versions `base` and `v2`; their files are uploaded from `test-data/EL-7675/compare-files-qa/base/` and `compare-files-qa/v2/` (see the README there for the expected chips).

---

## Test Data

| Field | Value |
|-------|-------|
| Skill | Compare Files QA |
| Binary changed | `assets/logo.png` (red in base, blue in v2) |
| Binary identical | `assets/same.png` |
| Over 50,000 characters | `references/long.md` (~60 KB) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open skill **Compare Files QA** → actions menu (⋮) → **Compare versions**, Base = `base`, Compare with = `v2`, click **Compare**. Click **Next**. | Files step opens. |
| 2 | Select `assets/logo.png` (Replaced). | Each column shows a card: icon, `logo.png`, size, Download; both cards have an orange frame; no text field and no Copy. |
| 3 | Click Download in each card and open the files. | base gives the red image, v2 the blue image. |
| 4 | Select `references/long.md`. | Cards with `<size> · too long to compare here`; no text editor. |
| 5 | Turn **Only changed** OFF and select `assets/same.png`. | Cards without the orange frame. |
| 6 | Check both version headers. | Save stays disabled; nothing can be edited on cards. |

---

## Expected Final State

No version data changed; downloads match their versions.

---

## Pass/Fail Criteria

**Pass:**
- Cards with correct name, size and Download; orange frame only when different.

**Fail:**
- Text diff or editor shown for binary/long files.
- Download returns the wrong version or fails.
