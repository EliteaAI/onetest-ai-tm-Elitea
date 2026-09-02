---
id: ELITEA-3106
title: "A Model-Retried Patch After Truncation Still Goes Through the Normal Hash-Guard Path"
priority: low
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, chat, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3106: A Model-Retried Patch After Truncation Still Goes Through the Normal Hash-Guard Path

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Low · **Type:** Functional

**Objective:** Confirm that if the model itself (not the user) re-attempts a patch tool call after a truncated first attempt — e.g. after "Continue" prompts it to retry — the retried call is evaluated fresh against the current hash/old_text state (normal conflict-guard rules apply), rather than being fast-tracked or treated as a resume of the earlier attempt. **Not testable from this session** — depends on the same unreproducible truncation scenario as [[ELITEA-3104]]/[[ELITEA-3105]], plus needing the model to actually choose to retry (a further layer of non-determinism).

---

## Preconditions

- A truncated first patch attempt, followed by a model-initiated retry of the same or a similar patch.

---

## Test Data

| Field | Value |
|-------|-------|
| Scenario | Truncated patch attempt → model retries the tool call after "Continue" |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Force a truncated first patch tool-call attempt. | No mutation applied. |
| 2 | Send "Continue"; observe whether/how the model retries the patch. | If retried, the retry is a normal fresh tool call. |
| 3 | Verify the retry is evaluated against current hash/old_text (subject to normal 409 guards if state has since changed). | Guards apply identically to any other patch call — no special-cased "resume" bypass. |

---

## Expected Final State

No bypass of the standard hash/old_text guards for a model-initiated retry after truncation.

---

## Actual Result — 2026-09-02

**Not testable from this session.** Requires both the unreproducible truncation scenario from [[ELITEA-3104]] and a non-deterministic model decision to retry the call after "Continue" — could not be reliably staged in the sandbox.

---

## Pass/Fail Criteria

**Pass:** A model-retried patch call after truncation is subject to the same hash/old_text guards as any fresh call.
**Fail:** A retried call bypasses guards (e.g. is treated as continuing/resuming the earlier truncated attempt with stale assumptions).

---

## Blocked / Fixture Needed

Requires reproducing a truncated tool-call attempt and then reliably prompting the model to retry it.
