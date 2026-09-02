---
id: ELITEA-3083
title: "Safe-Patch Call Where old_text Occurs 0 Times Is Rejected With No Side Effects"
priority: high
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3083: Safe-Patch Call Where old_text Occurs 0 Times Is Rejected

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Functional

**Objective:** Confirm a safe-patch call whose `old_text` does not appear anywhere in the current instructions is rejected with a 409 "found 0 matches" error, with no backup created and no change applied.

---

## Preconditions

- Sandbox agent (#414) with a draft version whose instructions are known.

---

## Test Data

| Field | Value |
|-------|-------|
| `old_text` | a phrase guaranteed absent from current instructions |
| `replacement` | any non-empty text |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the safe patch tool with a valid hash and an `old_text` known to be absent. | 409 "old_text must match exactly once; found 0 matches." |
| 2 | Re-read the draft version. | Instructions unchanged. |
| 3 | List versions. | No new backup created. |

---

## Expected Final State

Non-matching patches are rejected cleanly with no side effects.

---

## Actual Result — 2026-09-02

**Pass.** 409 with "found 0 matches" message; no backup; instructions unchanged.

---

## Pass/Fail Criteria

**Pass:** 409 with correct match-count message, zero side effects.
**Fail:** Call succeeds, wrong error, or any state change occurs.
