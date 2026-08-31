---
id: ELITEA-2968
title: "ADO Work Item Text Search – Out-of-Range `top` Hard-Errors Rather Than Being Clamped (Known Behavior)"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, known-limitation]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2968: ADO Work Item Text Search – Out-of-Range `top` Hard-Errors Rather Than Being Clamped (Known Behavior)

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Confirm the currently-observed behavior: a `top` value outside the valid range (`≤0` or `>50`) produces a hard tool error, rather than being silently clamped to the nearest valid value.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Test Data

| top value | Expected outcome |
|-----------|-------------------|
| `50` | Succeeds (ceiling, valid) |
| `51` | Hard error (one above ceiling) |
| `0` | Hard error |
| `-1` | Hard error |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `top=50` | Succeeds, returns up to 50 results |
| 2 | Call with `top=51` | Tool execution error, no results returned |
| 3 | Call with `top=0` | Tool execution error |
| 4 | Call with `top=-1` | Tool execution error |

---

## Expected Final State

Values within `[1, 50]` succeed; anything outside that range errors out instead of being clamped.

---

## Pass/Fail Criteria

**Pass:** `top=50` succeeds; `51`, `0`, and `-1` all hard-error — matches documented known behavior.
**Fail:** Any out-of-range value is silently clamped instead of erroring, or the valid ceiling has moved without a doc update.
