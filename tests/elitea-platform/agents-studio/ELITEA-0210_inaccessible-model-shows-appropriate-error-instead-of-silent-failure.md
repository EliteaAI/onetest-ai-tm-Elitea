---
id: ELITEA-0210
title: "Inaccessible Model Shows Appropriate Error Instead of Silent Failure"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0210: Inaccessible Model Shows Appropriate Error Instead of Silent Failure

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting a model the user/team does not have access to results in a clear, meaningful error rather than a silent failure or generic crash.

**Coverage:**
- Access-denied models produce a user-readable error
- No silent failure or blank response

## Preconditions

- A model exists in the dropdown that the current team cannot access (access controlled by team configuration)
- Published agent is open in chat

## Test Data

Model not accessible to the team (e.g. a model shown in list but restricted by team policy)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open model dropdown for published agent. | Full model list shown. |
| 2 | Select a model the team does not have access to (if identifiable). | Model selected in toolbar. |
| 3 | Send a test message. | Response is received. |
| 4 | Observe response content. | An informative error is shown (e.g. 'team not allowed to access model' or similar) — NOT a blank response or unhandled exception. |

## Expected Final State

An informative error is shown (e.g. 'team not allowed to access model' or similar) — NOT a blank response or unhandled exception.

## Pass/Fail Criteria

**Pass:**
- A clear, readable error message is shown explaining the access restriction
- Application remains stable (no crash)

**Fail:**
- Response is blank with no indication of failure
- Application crashes or shows an unhandled exception
