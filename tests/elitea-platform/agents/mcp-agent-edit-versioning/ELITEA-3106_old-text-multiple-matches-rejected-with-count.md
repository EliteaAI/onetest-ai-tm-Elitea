---
id: ELITEA-3106
title: "Safe-Patch Call Where old_text Occurs 2+ Times Is Rejected With the Correct Match Count"
priority: high
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3106: Safe-Patch Call Where old_text Occurs 2+ Times Is Rejected With the Correct Match Count

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Functional

**Objective:** Confirm a safe-patch call whose `old_text` matches two or more locations in the current instructions is rejected with a 409 reporting the actual match count (ambiguous replace target), with no backup created and no change applied.

---

## Preconditions

- Sandbox agent (#414) with a draft version whose instructions contain a deliberately repeated phrase.

---

## Test Data

| Field | Value |
|-------|-------|
| `old_text` | a phrase that appears exactly twice in current instructions |
| `replacement` | any non-empty text |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the safe patch tool with a valid hash and the doubly-occurring `old_text`. | 409 "old_text must match exactly once; found 2 matches." |
| 2 | Re-read the draft version. | Instructions unchanged. |
| 3 | List versions. | No new backup created. |

---

## Expected Final State

Ambiguous patches are rejected with an accurate match count and no side effects.

---

## Actual Result — 2026-09-02

**Pass.** 409 returned with the correct match count; no backup; instructions unchanged.

---

## Pass/Fail Criteria

**Pass:** 409 with the accurate match count, zero side effects.
**Fail:** Wrong/missing count, call succeeds, or any state change occurs.
