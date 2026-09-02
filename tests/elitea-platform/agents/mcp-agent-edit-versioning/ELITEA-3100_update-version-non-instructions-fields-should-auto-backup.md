---
id: ELITEA-3100
title: "[REGRESSION] Internal-MCP update_version Not Touching instructions Fails to Auto-Back-Up (Call Rejected Outright)"
priority: critical
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, bug]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3100: [REGRESSION] Internal-MCP update_version Not Touching instructions Fails to Auto-Back-Up

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm that an internal-MCP `update_version` (PUT) call that changes only non-`instructions` fields (e.g. `llm_settings`) still auto-creates a backup version before applying, per the documented "every internal-MCP mutating call auto-backs-up first" contract, and that the response includes `mcp_backup_version`.

---

## Preconditions

- Sandbox agent (#414) with a draft version.
- Ability to trigger an internal-MCP `update_version` call that changes only `llm_settings` (no `instructions` field in the body).

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | sandbox parent agent (#414) |
| Payload | `update_version` body with `llm_settings` changed only, no `instructions` key |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Via internal MCP, call `update_version` with a body that changes `llm_settings` only (`instructions` key absent). | Per design: call should succeed, auto-creating a backup version first, then applying the `llm_settings` change. |
| 2 | Inspect the response. | Expected: `mcp_backup_version` present; new `llm_settings` applied to the draft. |
| 3 | List versions for the agent. | Expected: exactly one new `mcp-backup-*` version. |

---

## Expected Final State

Per design, the draft's `llm_settings` should be updated and exactly one backup version should exist.

---

## Actual Result — 2026-09-02

**FAIL.** The internal-MCP `update_version` call was **rejected outright** — no backup was created and no field was updated, even though the request body contained no `instructions` key. This contradicts the documented contract (non-instructions internal-MCP `update_version` calls should still succeed with an auto-created backup). All P0/P1 checks that depend on a working non-instructions `update_version` path (tags regression checks ELITEA-3101–3103) are blocked by this defect.

**Suspected root cause (needs core-side confirmation):** the internal-MCP origin check on `update_version` appears to be rejecting the call unconditionally when the WSGI marker is set, rather than only when `instructions` is present in the body — i.e. the `'instructions' in raw_version_data` guard may not be gating the rejection correctly for internal-MCP requests.

---

## Pass/Fail Criteria

**Pass:** Non-instructions internal-MCP `update_version` call succeeds, creates a backup, applies the change, and returns `mcp_backup_version`.
**Fail:** Call is rejected/fails, or succeeds without creating a backup. **(Observed: rejected outright — see Actual Result.)**

---

## Notes

File this as a defect against issue #6018 / PR EliteaAI/elitea_core#378 — the implementation does not match its own documented contract for non-instructions internal-MCP `update_version` calls. This blocks live verification of the bundled tags-regression fix (ELITEA-3101–3103), since every internal-MCP `update_version` call currently fails regardless of whether `tags` is involved.
