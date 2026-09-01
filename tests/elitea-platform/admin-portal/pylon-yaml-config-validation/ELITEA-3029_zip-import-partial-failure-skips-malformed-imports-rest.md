---
id: ELITEA-3029
title: "Zip Import With One Malformed Config Skips Only That File; Others Import Successfully With No Caller-Facing Indication"
priority: medium
type: functional
module: pylon-yaml-config-validation
status: draft
execution_type: manual
tags: [admin, credentials, yaml-validation, issue:6268, gap]
requirements: [EliteaAI/elitea_issues#6268]
---

# ELITEA-3029: Zip Import With One Malformed Config Skips Only That File; Others Import Successfully With No Caller-Facing Indication

**Module:** Admin Portal / Pylon YAML Config Validation · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm the batch/zip import path (`api/v2/runtime_remote.py`, `action=="import_configs"`), patched in `admin#37` with a per-file `try: yaml.safe_load(...) except: continue` skip (not a hard failure), behaves as read directly from the diff: a malformed `.yml` file inside the zip is skipped (logged as a warning) while all other valid entries still import and fire their own `bootstrap_runtime_update` events — and the overall response is still `{"ok": True}` with no indication to the caller that anything was skipped.

---

## Preconditions

- Ability to construct and upload a zip archive of pylon/plugin `.yml` config files through the Admin Configuration import flow (or directly via the `import_configs` API action).
- At least 2 valid `.yml` configs plus 1 intentionally malformed `.yml` to include in the same archive.

---

## Test Data

| Field | Value |
|-------|-------|
| Zip contents | `valid_a.yml` (valid config), `valid_b.yml` (valid config), `broken.yml` (contains `password: fo: bar` unquoted — malformed) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Build the zip with the three files above and import it via the Admin Configuration import flow (or `POST action=import_configs`). | Import request completes. |
| 2 | Inspect the response. | Response is `{"ok": True}` — with **no** field listing which files, if any, were skipped. Confirm this is actually what's returned (this is the specific gap being verified). |
| 3 | Verify `valid_a.yml` and `valid_b.yml` were actually applied (their pylons/plugins show the new config; their respective `bootstrap_runtime_update` events fired). | Both valid configs imported successfully, independent of the broken one. |
| 4 | Verify `broken.yml`'s target pylon/plugin was **not** modified — its config remains whatever it was before the import (or empty/default, if it had none). | The malformed file's config is skipped, not partially written. |
| 5 | Check server logs for a warning referencing the skipped file. | A `log.warning()` is present identifying `broken.yml` (or its target) as skipped due to invalid YAML. |
| 6 | From the Admin Configuration UI (if the import flow is UI-driven), confirm whether the admin who performed the import is shown any indication that one file was skipped. | Document what's actually shown — per the code read, the response contains no skipped-file list, so the expectation is the admin sees only a generic success with no mention of the partial failure. This is the known UX/observability gap; confirm it's real rather than assuming. |

---

## Expected Final State

Two of three files import successfully; the malformed one is silently skipped server-side (logged, not surfaced to the caller); overall response reports success.

---

## Pass/Fail Criteria

**Pass (as a gap-confirmation test):** Behavior matches the code: valid files import, broken file is skipped and logged, response gives no indication of the partial failure to the caller.
**Fail:** Any valid file also fails to import (over-broad rejection); OR the broken file's config is partially/incorrectly written despite being "skipped"; OR the response actually does include skipped-file information, meaning this gap was already addressed elsewhere and the checklist should be updated.
