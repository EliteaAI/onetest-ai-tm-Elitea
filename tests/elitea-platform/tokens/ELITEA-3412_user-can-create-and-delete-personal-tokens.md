---
id: ELITEA-3412
title: "User Can Create and Delete Their Own Personal Access Tokens"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3412: User Can Create and Delete Personal Access Tokens

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm ordinary personal-token CRUD (create, list, delete) still works normally for a user after this feature has shipped — the new system token and its guards must not interfere with a user managing their own tokens.

**Coverage:** Regression check alongside AC — normal token management is unaffected by system-token provisioning

## Preconditions

- A logged-in user

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Personal Access Tokens page and create a new token with a normal, non-reserved name. | Token is created successfully and appears in the list. |
| 2 | Create a second personal token with a different name. | Both tokens now appear in the list. |
| 3 | Delete the first token. | Deletion succeeds; the token disappears from the list; the second token remains. |
| 4 | Delete the second (remaining) personal token. | Deletion succeeds; the personal token list is now empty. |

## Expected Final State

The user can freely create and delete their own personal tokens with no unexpected errors or interference from the system token.

## Pass/Fail Criteria

**Pass:**
- All create and delete operations on ordinary personal tokens succeed as expected

**Fail:**
- Any create or delete operation on a personal (non-system) token fails or behaves unexpectedly
