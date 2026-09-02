---
id: ELITEA-3102
title: "[BLOCKED by ELITEA-3078] Explicit tags: [] Still Clears Existing Tags"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, blocked]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3102: Explicit tags: [] Still Clears Existing Tags

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm an `update_version` PUT that explicitly sends `tags: []` still clears existing tags — preserving the "explicit empty list means clear" distinction from "omitted means leave unchanged" (see [[ELITEA-3101]]). **Blocked this session** by the same [[ELITEA-3078]] regression.

---

## Preconditions

- Sandbox agent version with at least one existing tag.
- Requires [[ELITEA-3078]] to be fixed first.

---

## Test Data

| Field | Value |
|-------|-------|
| Existing tags | at least one tag on the version |
| Payload | `update_version` body with `tags: []` explicitly |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Confirm the version has at least one tag (baseline). | Baseline confirmed. |
| 2 | Call internal-MCP `update_version` with `tags: []` explicitly in the body. | Call succeeds (once ELITEA-3078 is fixed). |
| 3 | Re-read the version's tags. | Empty — tags cleared. |

---

## Expected Final State

Explicit empty list still means "clear," distinct from omission.

---

## Actual Result — 2026-09-02

**Blocked, not testable.** Same root cause as [[ELITEA-3101]] — every internal-MCP `update_version` call failed outright this session.

---

## Pass/Fail Criteria

**Pass:** Explicit `tags: []` clears existing tags.
**Fail:** Tags are not cleared despite the explicit empty list.

---

## Blocked / Fixture Needed

Blocked on a fix for [[ELITEA-3078]].
