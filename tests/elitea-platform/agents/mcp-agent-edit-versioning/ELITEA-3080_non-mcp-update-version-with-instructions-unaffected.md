---
id: ELITEA-3080
title: "Non-Internal-MCP update_version With instructions Behaves Exactly as Before (No Forced Backup/409)"
priority: high
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3080: Non-Internal-MCP update_version With instructions Behaves Exactly as Before

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Functional

**Objective:** Confirm a regular UI/API `update_version` call (not originating from internal MCP dispatch) that includes `instructions` continues to work exactly as before this feature — no forced backup, no 409, no behavior change for normal users editing prompts in the Agent Builder UI. **Not testable from a Chat/internal-MCP session** — requires a direct UI or authenticated REST client call outside the MCP tool layer.

---

## Preconditions

- Direct access to the Agent Builder UI or an authenticated REST client (not routed through internal MCP dispatch).
- An agent with a draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | any test agent |
| Edit | change `instructions` directly via the Agent Builder's prompt editor, or a direct authenticated `PUT /version/...` call |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Edit an agent's instructions directly in the Agent Builder UI and save. | Save succeeds; no new `mcp-backup-*` version appears. |
| 2 | Alternatively, call `update_version` directly via an authenticated REST client (outside internal-MCP dispatch) with `instructions` in the body. | 2xx response; instructions updated; no 409; no backup created. |

---

## Expected Final State

Normal, non-MCP instruction edits are completely unaffected by this feature.

---

## Actual Result — 2026-09-02

**Not testable this session.** No non-MCP client/UI access was available from the Chat-based testing session used for the rest of this checklist — only internal-MCP tool calls could be exercised. Requires a follow-up pass using the Agent Builder UI directly or a REST client with a normal (non-internal) auth session.

---

## Pass/Fail Criteria

**Pass:** Non-MCP `update_version` with `instructions` behaves identically to pre-#6018 behavior (no forced backup, no 409).
**Fail:** Non-MCP callers are also forced into backup creation or blocked by the 409 rejection meant only for internal MCP.

---

## Blocked / Fixture Needed

Requires direct Agent Builder UI access or a non-MCP authenticated API client to execute; not reachable from within a Chat/internal-MCP-only test session.
