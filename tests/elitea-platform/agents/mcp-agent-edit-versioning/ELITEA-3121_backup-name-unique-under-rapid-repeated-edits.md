---
id: ELITEA-3121
title: "Backup Version Names Stay Unique Under Rapid Repeated Edits to the Same Version"
priority: low
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3121: Backup Version Names Stay Unique Under Rapid Repeated Edits

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Low · **Type:** Functional

**Objective:** Confirm backup version names remain unique and collision-free across two or more rapid, successive edits to the same version within the same second, relying on the microsecond-precision UTC timestamp in `mcp-backup-{version_id}-{timestamp}`. **Not conclusively testable this session** — the hash-guard (each edit requires the freshly-read post-previous-edit hash) naturally serializes calls, making a true same-second collision hard to force without direct timing control.

---

## Preconditions

- Ability to fire 2+ safe-patch calls against the same version in rapid succession, each with a freshly-read valid hash.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | sandbox parent agent (#414) |
| Edits | 2+ small, independent, valid patches fired back-to-back |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Perform edit 1 (read hash → patch). | Backup #1 created. |
| 2 | Immediately perform edit 2 (read new hash → patch), as fast as scripting allows. | Backup #2 created. |
| 3 | Compare the two backup names. | Distinct names, no unique-constraint failure on either call. |

---

## Expected Final State

No name collisions even under the fastest achievable back-to-back edit cadence.

---

## Actual Result — 2026-09-02

**Not conclusively testable this session.** Because each safe-patch call requires the current `instructions_sha256` (read fresh after the prior edit), calls are naturally serialized by the read-then-patch workflow, making a genuine same-microsecond-bucket race difficult to force manually. Two sequential edits performed during this session did each produce distinct backup names, but this doesn't stress the boundary condition the check is really after (true concurrent/same-second creation). Would need either a scripted tight loop with pre-fetched hashes replayed as fast as possible, or a direct unit-level test of `build_mcp_backup_version_name` with frozen/near-identical timestamps.

---

## Pass/Fail Criteria

**Pass:** All backup names remain distinct even under the fastest achievable repeated-edit cadence.
**Fail:** Any two backups from rapid successive edits share the same name (DB unique-constraint failure or silent overwrite).

---

## Blocked / Fixture Needed

Requires either a tight scripted loop capable of firing safe-patch calls faster than typical Chat-driven cadence, or a unit-level test against `build_mcp_backup_version_name` with controlled/frozen timestamps to force a true same-second scenario.
