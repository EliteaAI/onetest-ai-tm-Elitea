---
id: ELITEA-3107
title: "Nested (Pipeline) Agent Link Survives a Safe-Patch Edit to the Parent Agent"
priority: high
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3107: Nested (Pipeline) Agent Link Survives a Safe-Patch Edit to the Parent Agent

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Functional

**Objective:** Confirm that a safe-patch instructions edit to a parent agent that has a nested sub-agent configured does not break, detach, or corrupt the nested-agent link on the resulting draft version.

---

## Preconditions

- Sandbox parent agent (#414) with nested sub-agent (#415) configured.

---

## Test Data

| Field | Value |
|-------|-------|
| Parent agent | #414 |
| Nested sub-agent | #415 |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Confirm the parent's draft version has the nested sub-agent (#415) linked (baseline). | Baseline confirmed. |
| 2 | Perform a safe-patch instructions edit on the parent's draft version. | Edit succeeds; backup + updated draft created. |
| 3 | Re-inspect the updated draft version's nested-agent link. | Sub-agent #415 still linked, unchanged. |

---

## Expected Final State

Nested-agent configuration is unaffected by an instructions-only patch.

---

## Actual Result — 2026-09-02

**Pass.** Confirmed on the sandbox parent (#414)/sub-agent (#415) pair — the nested-agent link remained intact and functional after the safe-patch edit.

---

## Pass/Fail Criteria

**Pass:** Nested-agent link remains intact after the edit.
**Fail:** Link is broken, detached, or altered by the instructions edit.
