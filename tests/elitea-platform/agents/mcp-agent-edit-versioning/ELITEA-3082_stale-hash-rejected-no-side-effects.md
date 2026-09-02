---
id: ELITEA-3082
title: "Safe-Patch Call With a Stale expected_instructions_sha256 Is Rejected With No Side Effects"
priority: critical
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3082: Safe-Patch Call With a Stale expected_instructions_sha256 Is Rejected With No Side Effects

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm a safe-patch call using an `expected_instructions_sha256` that no longer matches the version's current instructions (changed since it was read) is rejected with HTTP 409 referencing "changed after they were read," leaving the draft unchanged and creating no backup.

---

## Preconditions

- Sandbox agent (#414) with a draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | sandbox parent agent (#414) |
| `expected_instructions_sha256` | a hash captured before an unrelated edit changed the instructions |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Read `instructions_sha256`, then change the instructions via another edit (invalidating the hash). | Instructions now differ from what the captured hash represents. |
| 2 | Call the safe patch tool using the now-stale hash. | 409 response referencing "changed after they were read." |
| 3 | Re-read the draft version. | Instructions unchanged from step 1's post-edit state. |
| 4 | List versions. | No new backup created by the rejected call. |

---

## Expected Final State

Stale-hash calls are cleanly rejected with zero side effects.

---

## Actual Result — 2026-09-02

**Pass.** 409 returned with the expected "changed after they were read" message; no backup created; draft instructions unchanged by the rejected call.

---

## Pass/Fail Criteria

**Pass:** 409 with correct message, zero side effects.
**Fail:** Call succeeds despite stale hash, or leaves partial state.
