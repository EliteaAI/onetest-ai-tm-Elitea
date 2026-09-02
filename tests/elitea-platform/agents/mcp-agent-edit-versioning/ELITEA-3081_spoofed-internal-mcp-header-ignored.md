---
id: ELITEA-3081
title: "Client-Supplied Header Spoofing the Internal-MCP Origin Is Ignored on Normal REST Calls"
priority: high
type: security
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api, security, needs-fixture]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3081: Client-Supplied Header Spoofing the Internal-MCP Origin Is Ignored

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Security

**Objective:** Confirm that a normal REST/UI client cannot forge internal-MCP origin by sending a custom HTTP header (e.g. `X-Internal-MCP-*`) — the origin marker is set only in-process via the server's own WSGI dispatch and must be un-spoofable from outside. **Not testable via the internal-MCP tool layer itself** — requires a raw HTTP client capable of injecting arbitrary headers directly against the REST API.

---

## Preconditions

- A raw HTTP client (e.g. curl/Postman) with a valid auth token, able to set arbitrary request headers.
- An agent with a draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| Header | `X-Internal-MCP-Request: true` (or similarly-named candidate header) |
| Call | `PUT` to `update_version` with `instructions` in the body, plus the spoofed header |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Send a normal authenticated `update_version` PUT with `instructions` in the body, with no special header. | Succeeds normally (no MCP restriction applies) — baseline. |
| 2 | Repeat the same call, adding a client-supplied header attempting to claim internal-MCP origin. | Behaves identically to step 1 — no 409, no forced backup. The header has no effect since the origin marker is WSGI-environ-only and never derived from request headers. |

---

## Expected Final State

Internal-MCP restrictions cannot be triggered or bypassed by any externally-controllable request data.

---

## Actual Result — 2026-09-02

**Not testable this session.** Raw HTTP header injection isn't possible through the internal-MCP tool interface used for this test pass. Requires a direct REST client test outside the Chat/MCP session.

---

## Pass/Fail Criteria

**Pass:** Spoofed header has zero effect on `update_version` behavior.
**Fail:** A client-supplied header can trigger (or bypass) internal-MCP-only restrictions.

---

## Blocked / Fixture Needed

Requires a raw authenticated HTTP client capable of custom headers, run outside the MCP tool session.
