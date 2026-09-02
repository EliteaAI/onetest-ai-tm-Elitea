---
id: ELITEA-3123
title: "[BLOCKED by ELITEA-3100] Partial update_version Omitting tags No Longer Wipes Existing Tags"
priority: high
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, blocked]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3123: Partial update_version Omitting tags No Longer Wipes Existing Tags

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Functional

**Objective:** Confirm a partial `update_version` PUT that omits `tags` entirely no longer clears existing tags on the version — this is the bundled regression fix for a prior Pydantic-default-`[]` bug. **Blocked this session** by the [[ELITEA-3100]] regression: every internal-MCP `update_version` call currently fails outright regardless of whether `tags` is involved, so this specific behavior could not be reached.

---

## Preconditions

- Sandbox agent version with at least one existing tag.
- Requires [[ELITEA-3100]] to be fixed first (internal-MCP `update_version` currently rejects all non-instructions calls).

---

## Test Data

| Field | Value |
|-------|-------|
| Existing tags | at least one tag on the version |
| Payload | `update_version` body omitting `tags` entirely, changing an unrelated field |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Confirm the version has at least one tag (baseline). | Baseline confirmed. |
| 2 | Call internal-MCP `update_version` with a body that omits `tags` but changes an unrelated field. | Call succeeds (once ELITEA-3100 is fixed); auto-backup created. |
| 3 | Re-read the version's tags. | Unchanged from baseline — tags are not wiped. |

---

## Expected Final State

Tags survive a partial update that doesn't mention them.

---

## Actual Result — 2026-09-02

**Blocked, not testable.** Every internal-MCP `update_version` call attempted this session failed outright per the [[ELITEA-3100]] regression, before reaching the tags-handling logic at all. Cannot be verified until that defect is fixed.

---

## Pass/Fail Criteria

**Pass:** Tags remain unchanged after a partial update omitting `tags`.
**Fail:** Tags are wiped despite being omitted from the request.

---

## Blocked / Fixture Needed

Blocked on a fix for [[ELITEA-3100]] (internal-MCP `update_version` rejecting calls that don't touch `instructions`).
