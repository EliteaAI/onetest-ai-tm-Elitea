---
id: ELITEA-3092
title: "old_text Containing Regex-Like Special Characters Is Matched Literally"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3092: old_text Containing Regex-Like Special Characters Is Matched Literally

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm `old_text` is matched as a plain literal substring, not interpreted as a regular expression — a phrase containing regex metacharacters (e.g. `.*`, parentheses) matches only its exact literal occurrence.

---

## Preconditions

- Sandbox agent (#414) with a draft version whose instructions contain a phrase with regex-like characters, e.g. `"handle (edge cases) and .* patterns"`.

---

## Test Data

| Field | Value |
|-------|-------|
| `old_text` | `"handle (edge cases) and .* patterns"` (literal, present exactly once) |
| `replacement` | different literal text |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the safe patch tool with the special-character `old_text`. | Call succeeds; only the exact literal phrase is replaced. |
| 2 | Inspect the resulting instructions. | No unintended matches from regex interpretation (e.g. `.*` did not greedily match unrelated text). |

---

## Expected Final State

Special characters in `old_text` behave as literal text, never as regex syntax.

---

## Actual Result — 2026-09-02

**Pass.** The special-character phrase was matched and replaced literally; no regex-style greedy/unintended matching observed.

---

## Pass/Fail Criteria

**Pass:** Literal, exact match/replace regardless of regex metacharacters present.
**Fail:** Any evidence of regex interpretation (wrong match, greedy match, or crash on invalid regex).
