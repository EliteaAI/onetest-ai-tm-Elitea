---
id: ELITEA-3117
title: "Malformed expected_instructions_sha256 Is Rejected With a 400 Before Any DB Query"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3117: Malformed expected_instructions_sha256 Is Rejected Before Any DB Query

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm `expected_instructions_sha256` values that are not exactly 64 hex characters (too short, too long, or containing non-hex characters) are rejected with a clear 400 validation error, before any database lookup occurs.

---

## Preconditions

- Sandbox agent (#414) with a draft version.

---

## Test Data

| Case | `expected_instructions_sha256` value |
|------|----------------------------------------|
| Too short | 32-char hex string |
| Too long | 128-char hex string |
| Non-hex | 64 chars including non-hex letters (e.g. `g`, `z`) or symbols |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the safe patch tool with a too-short hash. | 400 validation error. |
| 2 | Call with a too-long hash. | 400 validation error. |
| 3 | Call with a 64-char non-hex string. | 400 validation error. |
| 4 | For each case, confirm no backup/change occurred. | No side effects in any case. |

---

## Expected Final State

Malformed hashes never reach the DB-comparison logic; they fail fast on shape validation.

---

## Actual Result — 2026-09-02

**Pass.** All three malformed-hash cases were rejected with a 400 validation error prior to any DB work; no side effects.

---

## Pass/Fail Criteria

**Pass:** All malformed-shape cases rejected with 400, zero side effects.
**Fail:** Any malformed hash is accepted, or produces an unhandled server error rather than a clean validation error.
