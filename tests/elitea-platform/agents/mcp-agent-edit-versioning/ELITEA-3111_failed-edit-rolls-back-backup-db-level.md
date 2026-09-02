---
id: ELITEA-3111
title: "Backup Is Rolled Back Along With a Failed Edit (DB-Level Atomicity Check)"
priority: critical
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3111: Backup Is Rolled Back Along With a Failed Edit (DB-Level Atomicity Check)

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm that when a safe-patch (or internal-MCP `update_version`) call's underlying `applications_update_version` validation fails for an unrelated reason (e.g. invalid `llm_settings`) after the backup has already been cloned in-session, the whole transaction — including the just-cloned backup — rolls back. This must be verified with a **direct DB query** after the failed call, not just the HTTP response, since an orphaned backup would be invisible to a response-only check.

---

## Preconditions

- Direct DB read access (or an equivalent trusted admin API) to query `application_versions` for the target agent.
- Ability to trigger a downstream validation failure during an internal-MCP mutating call (e.g. deliberately invalid `llm_settings` payload) that occurs *after* the backup-clone step but before commit.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | sandbox parent agent (#414) |
| Payload | a patch/update call with an otherwise-valid instructions change plus a deliberately invalid unrelated field (e.g. malformed `llm_settings`) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Record the current count/list of versions for the agent (baseline). | Baseline captured. |
| 2 | Trigger an internal-MCP mutating call designed to fail validation after the backup-clone step. | Call fails (4xx/5xx), HTTP response shows no successful mutation. |
| 3 | Query the DB directly for the agent's versions. | Version count/list is **identical to the baseline** — no orphan `mcp-backup-*` version exists. |
| 4 | Re-read the draft version via API. | Unchanged from before the failed call. |

---

## Expected Final State

A failed edit never leaves an orphaned backup — the DB-level guarantee, not just the API-response guarantee, holds.

---

## Actual Result — 2026-09-02

**Not independently verifiable this session** — no direct DB access was available from the Chat/MCP tool session used for testing. However, across every failure-path case actually exercised (stale hash, 0/2+ matches, empty/no-op replacement — ELITEA-3104/3105/3106/3108/3109), no orphaned backup was observed via the API-level version listing in any case. This is corroborating but not conclusive evidence — a DB-level check is still needed to fully close this item, since an orphan could theoretically exist without surfacing through the listing API used.

---

## Pass/Fail Criteria

**Pass:** DB query after a failed edit shows zero orphaned backup versions.
**Fail:** A `mcp-backup-*` version exists in the DB with no corresponding successful edit.

---

## Blocked / Fixture Needed

Requires direct DB (or trusted admin API) access, and a way to force a downstream validation failure specifically after the backup-clone step (e.g. invalid `llm_settings` in the same request as a valid instructions patch, if the two are ever combinable) to properly exercise the rollback path rather than an earlier, pre-clone validation failure.
