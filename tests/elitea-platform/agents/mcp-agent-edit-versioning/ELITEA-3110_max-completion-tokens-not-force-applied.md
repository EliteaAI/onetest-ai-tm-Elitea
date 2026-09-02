---
id: ELITEA-3110
title: "20k Max Completion Tokens Is Not Force-Applied to Internal-MCP Calls (Out of Scope, Confirmed Intentional)"
priority: low
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, out-of-scope]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3110: 20k Max Completion Tokens Is Not Force-Applied to Internal-MCP Calls

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Low · **Type:** Functional

**Objective:** Confirm that a 20,000-token max-completion-tokens cap discussed as a possible mitigation elsewhere is **not** force-applied specifically to internal-MCP tool-call generations by this feature — this is explicitly out of scope for #6018 and was not implemented as part of it. Recorded to prevent a false assumption that this safeguard exists.

---

## Preconditions

- None — this is a scope-confirmation check, not a functional test of new behavior.

---

## Test Data

N/A.

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Review the #6018 implementation for any max-completion-tokens enforcement tied to internal-MCP calls. | No such enforcement is introduced by this feature. |
| 2 | Confirm with the team/PR description whether this was intentionally left out of scope. | Confirmed intentional — a separate, unimplemented consideration. |

---

## Expected Final State

No max-completion-tokens cap is force-applied by #6018; this remains a known, explicitly out-of-scope gap.

---

## Actual Result — 2026-09-02

**Confirmed intentional.** #6018 does not force-apply a 20k max-completion-tokens cap to internal-MCP generations; this was discussed as a separate potential mitigation but deliberately left out of this feature's scope.

---

## Pass/Fail Criteria

**Pass:** No max-completion-tokens enforcement is present, consistent with confirmed scope.
**Fail:** Unexpected enforcement is found (would indicate scope drift and needs re-documentation, not a defect).

---

## Notes

This is a scope-boundary record, not a defect-hunting test — captured so the absence of this safeguard isn't later mistaken for an oversight.
