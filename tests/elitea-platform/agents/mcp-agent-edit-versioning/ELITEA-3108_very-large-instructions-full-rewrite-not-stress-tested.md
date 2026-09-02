---
id: ELITEA-3108
title: "Full-Rewrite (replace_all) Behavior With Very Large Instructions Is Not Stress-Tested"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3108: Full-Rewrite (replace_all) Behavior With Very Large Instructions Is Not Stress-Tested

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that a `replace_all` full-rewrite patch behaves correctly (succeeds, produces a correct backup + hash, no truncation/corruption) when the source instructions are very large (e.g. tens of KB, approaching realistic prompt-size upper bounds). **Not stress-tested this session** — only moderate-size instructions were used in the sandbox agent.

---

## Preconditions

- An agent version with a very large `instructions` field (tens of KB).

---

## Test Data

| Field | Value |
|-------|-------|
| Instructions size | tens of KB (not yet constructed) |
| Patch mode | `replace_all` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Construct or locate a version with very large instructions. | Baseline established. |
| 2 | Perform a `replace_all` full-rewrite patch. | Edit succeeds; backup created with full original large instructions intact; draft updated with new content, no truncation. |
| 3 | Verify new `instructions_sha256` matches the new content exactly. | Hash matches. |

---

## Expected Final State

Full-rewrite patches scale correctly to large instruction sizes.

---

## Actual Result — 2026-09-02

**Not stress-tested this session.** Only moderate-size instructions were used throughout the sandbox testing; no deliberately oversized instructions payload was constructed to probe this boundary.

---

## Pass/Fail Criteria

**Pass:** Full-rewrite succeeds correctly and without truncation/corruption for very large instructions.
**Fail:** Truncation, corruption, timeout, or backup/hash mismatch occurs for large instructions.

---

## Blocked / Fixture Needed

Requires constructing a test agent version with deliberately large (tens-of-KB) instructions content.
