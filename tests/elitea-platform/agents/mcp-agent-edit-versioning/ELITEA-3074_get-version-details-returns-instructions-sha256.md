---
id: ELITEA-3074
title: "get_version_details Returns instructions_sha256 Matching sha256(instructions)"
priority: critical
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3074: get_version_details Returns instructions_sha256 Matching sha256(instructions)

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm that reading an application version via the internal MCP `get_version_details` tool returns an `instructions_sha256` field, and that its value equals the SHA-256 hex digest of the version's current `instructions` (or `sha256("")` when instructions is null/empty). This fingerprint is the optimistic-concurrency anchor for every subsequent safe-patch call.

---

## Preconditions

- An agent (application) with at least one draft version containing non-empty `instructions`.
- Access to trigger internal-MCP tool calls (e.g. via Chat asking the assistant to inspect/read the agent's configuration).

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | sandbox parent agent (#414) |
| Version | current draft version |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Via Chat/internal MCP, call `get_version_details` for the target version. | Call succeeds and returns version details including an `instructions_sha256` field. |
| 2 | Independently compute `sha256(instructions)` for the same version's current instructions text (e.g. via a script/tool outside the app). | Computed hash is a 64-character hex string. |
| 3 | Compare the computed hash to the `instructions_sha256` returned in step 1. | Values are identical. |
| 4 | Repeat against a version whose `instructions` is null/empty. | `instructions_sha256` equals `sha256("")`. |

---

## Expected Final State

`get_version_details` reliably exposes a correct content fingerprint for use by the safe patch tool.

---

## Actual Result — 2026-09-02

**Pass.** Verified against sandbox agent #414: `instructions_sha256` returned by `get_version_details` matched `sha256(instructions)` for the current draft version.

---

## Pass/Fail Criteria

**Pass:** Returned `instructions_sha256` always equals `sha256(instructions)` (or `sha256("")` for null/empty).
**Fail:** Hash is missing, malformed, or does not match the actual instructions content.
