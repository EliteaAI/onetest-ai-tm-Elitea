---
id: ELITEA-3126
title: "\"Continue\" No Longer Acts as a Resume Mechanism for In-Progress Mutations"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, chat, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3126: "Continue" No Longer Acts as a Resume Mechanism for In-Progress Mutations

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that sending "Continue" in Chat after a truncated/interrupted agent-instructions edit does **not** resume or complete the interrupted mutation — the redefined semantics treat "Continue" as a fresh conversational turn, not a mutation-resume trigger. **Not testable this session** — requires reproducing a live Chat UI truncation scenario mid-edit, which wasn't reproducible without direct control over generation length/interruption timing.

---

## Preconditions

- Live Chat UI session with an agent capable of an internal-MCP edit whose tool-call emission can be truncated (e.g. via a very long generation hitting a token/time limit).

---

## Test Data

| Field | Value |
|-------|-------|
| Scenario | An instructions-edit tool call that gets cut off mid-emission |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Trigger an edit whose tool-call response is truncated before completion. | No mutation applied (partial/invalid tool call is dropped). |
| 2 | Send "Continue" in the same conversation. | Model treats it as a new turn; does not automatically re-attempt or complete the original truncated mutation. |
| 3 | Verify the version's instructions and hash. | Unchanged from before step 1 (no partial or resumed mutation occurred). |

---

## Expected Final State

No mutation completes via a "Continue" resume path; the version is left exactly as it was before the truncated attempt.

---

## Actual Result — 2026-09-02

**Not testable from this session.** Reproducing a genuine mid-emission truncation of a tool call requires either an unusually long generation that hits a hard token/time limit, or artificial interruption of the live Chat UI stream — neither was reliably reproducible in the sandbox during this session.

---

## Pass/Fail Criteria

**Pass:** "Continue" never causes a previously truncated/interrupted mutation to complete or partially apply.
**Fail:** Sending "Continue" resumes and completes an edit that was cut off mid-emission.

---

## Blocked / Fixture Needed

Requires a live Chat UI scenario where a tool-call emission can be reliably truncated (e.g. forcing a token/time-limit cutoff mid-call) to observe "Continue" behavior afterward.
