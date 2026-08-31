---
id: ELITEA-2969
title: "ADO Work Item Text Search – Out-of-Range `skip` Hard-Errors Rather Than Being Clamped (Known Behavior)"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, known-limitation]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2969: ADO Work Item Text Search – Out-of-Range `skip` Hard-Errors Rather Than Being Clamped (Known Behavior)

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Confirm the currently-observed behavior: a `skip` value outside the valid range (`<0` or `>1000`) produces a hard tool error, rather than being silently clamped.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Test Data

| skip value | Expected outcome |
|------------|-------------------|
| `1000` | Succeeds (ceiling, valid) |
| `1001` | Hard error (one above ceiling) |
| `-1` | Hard error |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `skip=1000` | Succeeds |
| 2 | Call with `skip=1001` | Tool execution error, no results returned |
| 3 | Call with `skip=-1` | Tool execution error |

---

## Expected Final State

Values within `[0, 1000]` succeed; anything outside that range errors out instead of being clamped.

---

## Pass/Fail Criteria

**Pass:** `skip=1000` succeeds; `1001` and `-1` hard-error — matches documented known behavior.
**Fail:** Any out-of-range value is silently clamped instead of erroring, or the valid ceiling has moved without a doc update.
