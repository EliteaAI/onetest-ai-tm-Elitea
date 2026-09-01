---
id: ELITEA-3045
title: "A Runtime Per-Call Headers Argument Named Authorization Is Hard-Rejected, Not Silently Overridden"
priority: high
type: security
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6002, nfr:security, api, gap]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3045: A Runtime Per-Call Headers Argument Named Authorization Is Hard-Rejected, Not Silently Overridden

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** High · **Type:** Security

**Objective:** Confirm a **distinct, stricter** protection from [[ELITEA-3043]]/[[ELITEA-3044]]. Those cover *configured* additional headers, which are silently overridden. This test covers a **per-call runtime argument**: if the OpenAPI tool's call schema accepts a `headers` argument at invocation time (as confirmed in the Rust replatform worker's `request_body_and_credential_header_overrides_are_strict` test, hard-rejecting with `OpenApiClientErrorCode::InvalidInput`), an agent/LLM attempting to slip an `Authorization` override in through that argument must fail loudly (an explicit error), not silently override or silently succeed. Since this was only confirmed in the Rust replatform backend (not yet the primary `elitea-sdk`/legacy execution path used by `stage.elitea.ai`), first confirm whether an equivalent runtime `headers` argument is even reachable on the live platform; if so, verify it has the same hard-reject behavior. If no such runtime argument path exists on the live platform, document that as the actual (safer, since there's no argument to exploit) state rather than assuming parity with the Rust worker.

---

## Preconditions

- An OpenAPI credential with Authentication Method = API Key/Bearer configured with a real key, and a toolkit built on it.
- Access to invoke the toolkit's operation with explicit per-call arguments (e.g. via a direct tool-call API, or by prompting the agent to pass a `headers` argument if the tool schema exposes one).

---

## Test Data

| Field | Value |
|-------|-------|
| Primary auth | API Key/Bearer, real key `real-bearer-token` |
| Runtime argument attempt | `headers: {"Authorization": "attacker-value"}` passed at tool-call time |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Inspect the tool's call schema/parameters for this OpenAPI operation. | Document whether a `headers` (or equivalent) argument is exposed at call time on the live platform. |
| 2 | If exposed, invoke the tool passing `headers: {"Authorization": "attacker-value"}` as a call argument. | Document the actual result. |
| 3 | If a rejection occurs, inspect the error. | Expect a hard, explicit error (e.g. invalid-input class), not a silent override and not a silent success using the attacker value. |
| 4 | If no such argument is exposed at all on the live platform, note this explicitly. | This is the safer outcome — there's no argument surface to exploit, so this specific gap doesn't apply to the primary execution path. |

---

## Expected Final State

Either there is no runtime `headers` argument surface on the live platform (safe by absence), or such an argument exists and any attempt to override `Authorization` through it is hard-rejected with an explicit error — never silently accepted or silently overridden.

---

## Pass/Fail Criteria

**Pass:** No runtime `headers` argument exists on the live platform, OR one exists and an `Authorization` override attempt through it is hard-rejected with an explicit error.
**Fail:** A runtime `headers` argument exists and an `Authorization` override attempt through it either succeeds (attacker value sent) or is silently swallowed with no error surfaced.
