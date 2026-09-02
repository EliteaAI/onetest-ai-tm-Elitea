---
id: ELITEA-3097
title: "Backup Version's shared_id/shared_owner_id Are Reset to None Even for a Shared-Origin Source"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3097: Backup Version's shared_id/shared_owner_id Are Reset to None

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm a backup version created from a source version that had `shared_id`/`shared_owner_id` set (i.e. the source was originally shared/cloned from elsewhere) has both fields reset to `None` in the backup — a backup is a new local version, not a reference to the shared origin. **Not tested this session** — no shared-origin version was available in the sandbox.

---

## Preconditions

- A version that was originally created by sharing/cloning from another project/owner (has non-null `shared_id`/`shared_owner_id`).

---

## Test Data

| Field | Value |
|-------|-------|
| Source version | one with `shared_id`/`shared_owner_id` set |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Confirm the source version's `shared_id`/`shared_owner_id` are non-null (baseline). | Baseline confirmed. |
| 2 | Trigger an internal-MCP edit that creates a backup of that version. | Backup created. |
| 3 | Inspect the backup version's `shared_id`/`shared_owner_id`. | Both are `None`, regardless of the source's values. |

---

## Expected Final State

Backups never carry forward a shared-origin reference.

---

## Actual Result — 2026-09-02

**Not tested this session.** No shared/cloned-origin version existed in the sandbox project to use as a source. Requires constructing (or locating) a version with `shared_id`/`shared_owner_id` set before executing.

---

## Pass/Fail Criteria

**Pass:** Backup's `shared_id`/`shared_owner_id` are always `None`.
**Fail:** Either field is copied forward from the shared-origin source.

---

## Blocked / Fixture Needed

Requires a version with a non-null `shared_id`/`shared_owner_id` (e.g. one shared into the sandbox project from another) before execution.
