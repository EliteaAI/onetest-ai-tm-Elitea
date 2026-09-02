---
id: ELITEA-2847
title: "Verify scripts containing <, </, or <!-- in JS content execute correctly"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, comm:feedback, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6176, EliteaAI/elitea_issues#6512]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An artifact bucket exists and is available for file upload

> ⚠️ **Known bug (#6512):** these cases currently fail silently — the script block is skipped with no error. Fix is pending; this test targets the intended final (fixed) behavior.
>
> ℹ️ Supersedes `ELITEA-2725_script-tags-do-not-execute-in-preview-mode.md`, which asserts the pre-fix behavior. This test case is the current, actual coverage for this scenario as of 2026-09-02; `ELITEA-2725` should be re-validated/deprecated once #6176 ships.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | `less-than-edge-cases.html` |
| Case A | `'<1 month'` — `<` + letter in string |
| Case B | `'<1 month'` via Unicode escape workaround |
| Case C | `a <= b` |
| Case D | `'</div>'` — `</` sequence |
| Case E | `'<div>'` — `<` + letter |
| Case F | `// comment with < b` |
| Case G | `x << 2` |
| Case H | `<!--` bare and `<!-- ... -->` with same-line closing |
| Case I | `/<\w+>/` — `<` + letter in regex |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `less-than-edge-cases.html` to a bucket and open in Preview mode | Diagnostic cases render |
| 2 | Review Case A, D, E, H, I results | All show **PASS** |
| 3 | Review Case B, C, F, G results | All show **PASS** |
| 4 | Check for error banners | No error banner is shown for any case |

## Expected Final State

All nine cases execute and report PASS — the parser no longer mis-parses `<`, `</`, or `<!--` inside script content.

## Pass/Fail Criteria

**Pass:**
- All 9 cases (A–I) show PASS, no error banner

**Fail:**
- Any of Cases A, D, E, H, I show NOT RUN/skipped (regression to pre-fix bug #6512 behavior)
