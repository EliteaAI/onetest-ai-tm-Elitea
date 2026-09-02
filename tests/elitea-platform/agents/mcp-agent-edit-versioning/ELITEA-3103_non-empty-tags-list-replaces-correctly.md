---
id: ELITEA-3103
title: "[BLOCKED by ELITEA-3078] Non-Empty tags List Correctly Replaces the Tag Set"
priority: low
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, blocked]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3103: Non-Empty tags List Correctly Replaces the Tag Set

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Low · **Type:** Functional

**Objective:** Confirm an `update_version` PUT sending a non-empty `tags` list correctly replaces the version's tag set (pre-existing, unchanged-by-this-feature behavior). **Blocked this session** by the same [[ELITEA-3078]] regression.

---

## Preconditions

- Sandbox agent version with an existing (different) tag set.
- Requires [[ELITEA-3078]] to be fixed first.

---

## Test Data

| Field | Value |
|-------|-------|
| Existing tags | `["old-tag"]` |
| Payload | `update_version` body with `tags: ["new-tag-a", "new-tag-b"]` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Confirm the version's existing tag set (baseline). | Baseline confirmed. |
| 2 | Call internal-MCP `update_version` with a new non-empty `tags` list. | Call succeeds (once ELITEA-3078 is fixed). |
| 3 | Re-read the version's tags. | Exactly the new list; old tags fully replaced. |

---

## Expected Final State

Non-empty `tags` replaces the set as before — unaffected by this feature.

---

## Actual Result — 2026-09-02

**Blocked, not testable.** Same root cause as [[ELITEA-3101]]/[[ELITEA-3102]].

---

## Pass/Fail Criteria

**Pass:** Tag set is fully replaced by the new non-empty list.
**Fail:** Replacement is partial, merged, or fails.

---

## Blocked / Fixture Needed

Blocked on a fix for [[ELITEA-3078]].
