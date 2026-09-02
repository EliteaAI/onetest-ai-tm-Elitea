---
id: ELITEA-3098
title: "Backup Version's status Is Always draft Regardless of Source Status"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3098: Backup Version's status Is Always draft

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm a backup version's `status` field is always `draft`, regardless of the source version's status (other than `published`/`embedded`, which block the edit entirely before a backup is ever attempted — see [[ELITEA-3088]]).

---

## Preconditions

- A source version with a non-`published`/non-`embedded` status (e.g. `draft`).

---

## Test Data

| Field | Value |
|-------|-------|
| Source version status | `draft` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Confirm the source version's status. | `draft` (baseline). |
| 2 | Trigger an internal-MCP edit that creates a backup. | Backup created. |
| 3 | Inspect the backup version's `status`. | `draft`. |

---

## Expected Final State

Backup status is consistently `draft`.

---

## Actual Result — 2026-09-02

**Not explicitly re-verified as a standalone check this session**, but consistent with observed behavior across every successful safe-patch case exercised (ELITEA-3074–3077, 3091–3096) — every backup created during this session showed `status: draft`, matching the documented contract. Treated as a passing observation rather than a dedicated isolated test; a source version with a differing (non-published/embedded) status was not specifically tried.

---

## Pass/Fail Criteria

**Pass:** Backup `status` is `draft` in all observed cases.
**Fail:** Any backup is created with a non-`draft` status.
