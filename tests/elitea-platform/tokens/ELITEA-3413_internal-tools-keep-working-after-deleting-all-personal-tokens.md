---
id: ELITEA-3413
title: "Internal Tools Requiring a Token Keep Working After All Personal Tokens Are Deleted"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, runtime-fallback]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3413: Internal Tools Keep Working After Deleting All Personal Tokens

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm that once a user deletes every personal token they have, product features that internally require a token on the user's behalf (Support Assistant, code node calls, other integrated functions) keep working — this is the end-to-end, product-level proof of the runtime fallback to the system token, exercised through real features rather than a direct API/RPC check.

**Coverage:** AC — runtime fallback to system token when no usable PAT exists, verified through an actual user-facing flow

## Preconditions

- A user with at least one personal token, so it can be deleted as part of the test
- Access to a feature that internally needs a token (e.g. Support Assistant, a code node in a pipeline, or another integrated function that previously required a PAT)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the feature under test (e.g. Support Assistant) works normally while the user still has personal token(s). | Feature works as expected. |
| 2 | Delete all of the user's personal tokens (via the Personal Access Tokens page). | Personal token list is now empty. |
| 3 | Use the same feature again (e.g. ask Support Assistant something, or run the pipeline/code node). | Feature still works normally — no "token not found"-style error, despite the user having zero personal tokens. |
| 4 | Repeat step 3 for at least one additional integrated feature that relies on a token internally, if available. | Same result — works via the fallback system token. |

## Expected Final State

Deleting all personal tokens does not break any feature that needs to authenticate as the user internally — the system token fallback keeps them working.

## Pass/Fail Criteria

**Pass:**
- Every tested internal-token-dependent feature continues to work after all personal tokens are deleted

**Fail:**
- Any feature errors out (e.g. "User token not found") after the user's personal tokens are all deleted
