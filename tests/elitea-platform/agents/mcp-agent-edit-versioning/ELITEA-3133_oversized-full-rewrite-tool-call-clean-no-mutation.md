---
id: ELITEA-3133
title: "Full-Rewrite Tool Call Too Large to Emit Results in a Clean No-Mutation Outcome"
priority: low
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3133: Full-Rewrite Tool Call Too Large to Emit Results in a Clean No-Mutation Outcome

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Low · **Type:** Functional

**Objective:** Confirm that if the model attempts a `replace_all` full-rewrite whose payload is too large for it to emit in a single tool call (hitting a generation/context limit before the call completes), the outcome is a clean no-mutation (no partial patch applied, no orphaned backup) rather than a corrupted or partially-applied edit. **Not specifically tested this session** — no scenario was constructed where the model's full-rewrite payload itself exceeded emission limits.

---

## Preconditions

- An agent whose instructions are large enough that a full-rewrite tool call's `replacement` payload risks exceeding a single-call emission limit.

---

## Test Data

| Field | Value |
|-------|-------|
| Scenario | `replace_all` full-rewrite with a replacement payload large enough to risk truncated emission |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Construct a scenario likely to produce an oversized full-rewrite tool-call payload. | Model attempts the call. |
| 2 | Observe whether the tool call is truncated/malformed before completion. | If truncated, no mutation is applied — clean no-op. |
| 3 | Verify no orphaned backup or partial instructions content resulted. | Draft version unchanged from before the attempt. |

---

## Expected Final State

An oversized full-rewrite attempt that can't be fully emitted fails cleanly with zero side effects.

---

## Actual Result — 2026-09-02

**Not specifically tested this session.** No scenario was constructed where the model's own full-rewrite tool-call payload risked exceeding single-call emission limits; related but distinct from the large-source-instructions case in [[ELITEA-3108]].

---

## Pass/Fail Criteria

**Pass:** An oversized full-rewrite attempt that fails to emit completely results in zero side effects (no partial patch, no orphaned backup).
**Fail:** A truncated/malformed oversized tool call results in a partially-applied edit or an orphaned backup.

---

## Blocked / Fixture Needed

Requires deliberately constructing a full-rewrite payload large enough to risk incomplete tool-call emission, and a way to observe the resulting state precisely.
