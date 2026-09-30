---
id: ELITEA-3539
title: "_ensure_backend Fallback Produces the Same OAuth-Required Message as the Toolkit-Level Guard"
priority: high
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3539: _ensure_backend Fallback Produces the Same OAuth-Required Message as the Toolkit-Level Guard

**Module:** Outlook Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that if the toolkit-level OAuth guard is bypassed or not yet initialized when a tool call reaches the backend directly, the `_ensure_backend` fallback check produces the same clear OAuth-required message documented in ELITEA-3519, rather than a different/inconsistent error.

## Preconditions

- A toolkit linked to an unauthorized Outlook credential (as in ELITEA-3519)
- A way to invoke an individual tool method directly (e.g. via a Pipeline step that calls the tool without going through the standard toolkit-level guard path, if such a path exists)

## Test Data

- Unauthorized Outlook credential/toolkit from ELITEA-3519

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke a tool directly through a path that reaches `_ensure_backend` without having passed through the toolkit-level guard (e.g. a lower-level Pipeline step invocation) | Call is intercepted by `_ensure_backend` |
| 2 | Compare the returned error text to the toolkit-level guard's message from ELITEA-3519 | Both paths return the same OAuth-required message content |

## Expected Final State

Both the proactive toolkit-level guard and the lazy `_ensure_backend` fallback produce identical, clear OAuth-required messaging.

## Pass/Fail Criteria

**Pass:**
- `_ensure_backend` fallback message matches the toolkit-level guard message

**Fail:**
- The two paths produce different, inconsistent, or unclear error messages
