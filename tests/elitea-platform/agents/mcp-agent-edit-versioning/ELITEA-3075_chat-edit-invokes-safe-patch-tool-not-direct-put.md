---
id: ELITEA-3075
title: "Chat-Driven Instruction Edit Invokes the Safe Patch Tool, Not a Direct instructions PUT"
priority: critical
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3075: Chat-Driven Instruction Edit Invokes the Safe Patch Tool, Not a Direct instructions PUT

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm that when the model is asked in Chat to edit an agent's system prompt, it follows the documented workflow (`get_version_details` → copy `instructions_sha256` → call the safe patch tool) rather than attempting a direct `update_version` PUT with `instructions` in the body.

---

## Preconditions

- Sandbox agent with an existing system prompt/instructions.
- Ability to observe the sequence of internal-MCP tool calls made during a Chat turn (e.g. tool-call trace/log).

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | sandbox parent agent (#414) |
| Chat request | "Update this agent's instructions to also mention X" |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | In Chat, ask the assistant to edit the target agent's instructions. | Assistant begins the edit workflow. |
| 2 | Inspect the tool-call sequence. | `get_version_details` is called first (or `instructions_sha256` is otherwise obtained), followed by the safe patch tool — no `update_version` call carrying `instructions` in its body precedes it. |
| 3 | Confirm the edit completes successfully via the patch tool. | Instructions are updated; no 409 from a rejected direct PUT is observed in the sequence. |

---

## Expected Final State

The model's tool-use behavior matches the safe patch tool's own `mcp_description` workflow guidance; no direct-instructions PUT attempt occurs.

---

## Actual Result — 2026-09-02

**Pass.** Observed tool-call sequence consistent with the documented workflow guidance; no direct-instructions PUT attempted before the patch tool call.

---

## Pass/Fail Criteria

**Pass:** Safe patch tool is used for the instructions edit; no direct `instructions`-bearing PUT attempt precedes it.
**Fail:** Model attempts (or the system allows) a direct `update_version` PUT with `instructions` for an internal-MCP-driven edit.
