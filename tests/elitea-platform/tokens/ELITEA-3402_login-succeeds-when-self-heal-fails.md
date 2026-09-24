---
id: ELITEA-3402
title: "Login Still Succeeds When Self-Heal Token Provisioning Fails"
priority: medium
type: negative
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, resilience]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3402: Login Succeeds Even If Self-Heal Provisioning Fails

**Module:** Tokens · **Priority:** Medium · **Type:** Negative

**Objective:** Confirm that a failure while self-healing a missing system token during login (DB error, RPC unavailable, version skew where an older `auth_core` doesn't yet expose `ensure_system_token`) never blocks or fails the login itself — the failure is caught, logged as a WARNING, and login proceeds normally. This directly protects against the exact failure mode this feature was built to prevent (a user locked out or degraded because of token plumbing).

**Coverage:** Design detail from `auth_init`#2 — bare `except:` around the self-heal call, login proceeds regardless

## Preconditions

- Ability to simulate the `ensure_system_token` RPC failing or being unavailable during login (e.g. stop/downgrade the `auth_core` service, or inject a failure at the RPC layer in a test environment)
- A test user with no existing system token

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Make the `auth_ensure_system_token` RPC call fail or be unreachable (simulated). | RPC call will error when invoked. |
| 2 | Log in as the test user. | Login still succeeds — user reaches the app normally, no error surfaced to the user. |
| 3 | Check server logs for the login flow. | A WARNING-level log entry is present (e.g. "Could not ensure system token for user {user_id}") with a traceback; no ERROR/CRITICAL escalation, no crash. |
| 4 | Restore the RPC to working order and log in again as the same user. | Login succeeds and this time the system token is successfully created (self-heal now works). |

## Expected Final State

A token-provisioning failure during login degrades gracefully — it's logged, but never blocks authentication.

## Pass/Fail Criteria

**Pass:**
- Login succeeds despite the simulated provisioning failure; failure is only visible as a server-side WARNING log
- A later successful login (once the dependency is healthy again) does complete the self-heal

**Fail:**
- Login fails, hangs, or surfaces an error to the user because of the provisioning failure
- The failure escalates unhandled (unlogged exception, crash) instead of being caught and logged
