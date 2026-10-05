---
id: ELITEA-3691
title: "Usage mode switch (off/observe/enforce) is independent of tracing state; enforce fails closed on Redis/Postgres outage"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, error-handling, mode-switching]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6573"]
---

# ELITEA-3691: Usage mode switch (off/observe/enforce) is independent of tracing state; enforce fails closed on Redis/Postgres outage

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify usage metering is gated only by its own mode switch (`off` / `observe` / `enforce`), independent of tracing/analytics-export state, and that behavior under a Redis/Postgres outage differs correctly by mode: `off`/`observe` log a warning and let predicts continue; `enforce` fails closed (predicts stop) — this is deliberate, intended behavior per #6573, not a bug.

---

## Preconditions

- Logged in to {{base_url}} with admin access to toggle the usage mode setting and tracing/analytics-export setting independently.
- Ability to simulate or trigger a Redis/Postgres outage in the test environment (coordinate with environment owner if needed — this may be a lower-priority manual/exploratory step if outage simulation isn't readily available).

---

## Test Data

| Field | Value |
|-------|-------|
| Usage modes | off, observe, enforce |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Disable tracing/analytics-export while usage mode is `observe`. | Tracing is off. |
| 2 | Make an LLM call (e.g. a chat message). | A `usage_event` row still appears despite tracing being disabled — confirms usage gating is independent of tracing. |
| 3 | Set usage mode to `off` or `observe`, then simulate a Redis/Postgres outage. | A warning is logged. |
| 4 | Attempt a predict (chat/agent call) during the simulated outage. | Predict continues uninterrupted despite the outage. |
| 5 | Set usage mode to `enforce`, then simulate the same outage. | A warning/error is logged. |
| 6 | Attempt a predict during the simulated outage under `enforce`. | Predict fails closed (stops) rather than continuing unmetered. |

---

## Expected Final State

Usage rows appear regardless of tracing state; outage behavior correctly differs by mode — continue in `off`/`observe`, fail closed in `enforce`.

---

## Pass/Fail Criteria

**Pass:**
- Usage rows are recorded with tracing disabled.
- `off`/`observe` continue predicts through an outage; `enforce` stops predicts through the same outage.

**Fail:**
- Usage recording depends on tracing being enabled.
- `enforce` allows predicts to continue unmetered during an outage (this is the specific, named risk per #6573), or `off`/`observe` incorrectly block predicts during an outage.
