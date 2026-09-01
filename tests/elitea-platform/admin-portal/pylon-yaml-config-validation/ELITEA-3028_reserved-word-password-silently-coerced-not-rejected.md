---
id: ELITEA-3028
title: "Unquoted Reserved-Word Password (yes/no/true/false) Is Silently Coerced to Boolean, Not Caught by Validation"
priority: high
type: functional
module: pylon-yaml-config-validation
status: draft
execution_type: manual
tags: [admin, credentials, yaml-validation, issue:6268, gap]
requirements: [EliteaAI/elitea_issues#6268]
---

# ELITEA-3028: Unquoted Reserved-Word Password (yes/no/true/false) Is Silently Coerced to Boolean, Not Caught by Validation

**Module:** Admin Portal / Pylon YAML Config Validation · **Priority:** High · **Type:** Functional

**Objective:** Confirm a known gap in the shipped fix: `yaml.safe_load()` only catches **syntax** errors, not semantically-surprising-but-syntactically-valid values. Under YAML 1.1 rules (which PyYAML's `safe_load` follows), an unquoted `yes`, `no`, `true`, `false`, `null`, or `~` parses to a boolean/null, not the literal string. If the password-entry path doesn't quote these values, a password that is literally the word `yes` (for example) would be silently stored as the boolean `True`, not the string `"yes"` — a **silent data-corruption risk distinct from a parse error**, which the new validation checkpoint does **not** detect (because `password: yes` is valid YAML).

---

## Preconditions

- Logged in as an ELITEA admin user with access to Admin → Configuration raw YAML editor.

---

## Test Data

| Field | Value |
|-------|-------|
| Raw YAML edit | `password: yes` (unquoted) — repeat with `no`, `true`, `false` if time permits |

---

## Steps

| # | Action | Expected Result / What To Actually Observe |
|---|--------|----------------------------------------------|
| 1 | Open the raw YAML editor, set `password: yes` (unquoted), Save. | Save succeeds with no error — this is valid YAML syntax, so `yaml.safe_load()` does not reject it. |
| 2 | Reload and inspect the stored/parsed value (via any available means — API GET, admin UI display, or a downstream consumer of this credential). | ⚠️ Document what the actual stored/used value is: the boolean `True`, or the string `"yes"`. If the value used at runtime is the boolean `True` rather than the literal string `"yes"`, this confirms the coercion gap. |
| 3 | If a downstream credential consumer exists (e.g. the associated toolkit tries to authenticate using this password), attempt authentication with the literal password `yes`. | Document whether authentication succeeds or fails — if the stored value is `True` (boolean) rather than `"yes"` (string), authentication using the literal string `yes` would likely fail or behave unexpectedly, since the comparison is against a different type/value than what was "saved." |
| 4 | Repeat for `no`, `true`, `false` if time permits. | Same coercion behavior expected for each YAML 1.1 boolean-like token. |

---

## Expected Final State

This test documents the actual behavior of a known, unmitigated gap — it is not expected to "pass" in the sense of the fix correctly handling this case, since AC5/edge-case coverage was never implemented for this specific scenario. Record the observed behavior precisely so it can be filed as a follow-up issue if confirmed.

---

## Pass/Fail Criteria

**Pass (as a confirmation test, not a feature-works test):** Confirms the coercion happens as predicted from reading `runtime_pylons_config.py`'s validation code (syntax-only `yaml.safe_load()`), i.e. the password is silently stored/used as a boolean rather than the literal string — documenting the gap accurately.
**Fail:** The actual behavior differs from what the code predicts (e.g. some other layer already quotes/escapes reserved words before they reach this handler, making the gap not actually reachable) — if so, correct the checklist/finding rather than assuming the gap is real without confirmation.
