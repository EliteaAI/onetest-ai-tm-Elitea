---
id: ELITEA-3515
title: "Mailbox Field Defaults Correctly When Left Blank"
priority: medium
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3515: Mailbox Field Defaults Correctly When Left Blank

**Module:** Outlook Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the optional `mailbox` field defaults to the signed-in user's own mailbox (`/me`) when not set.

## Preconditions

- N/A

## Test Data

- Mailbox field: left empty

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create an Outlook credential leaving the Mailbox field empty | Credential is created |
| 2 | Authorize and test the connection | Connection succeeds |
| 3 | Perform a mail operation (e.g. `list_messages`) via a toolkit using this credential | Operation resolves against the signed-in user's own mailbox, not an error about a missing mailbox target |

## Expected Final State

Mail operations succeed against the authenticated user's own mailbox with no `mailbox` value configured.

## Pass/Fail Criteria

**Pass:**
- Operations succeed against `/me` when Mailbox is blank

**Fail:**
- An error about a missing/invalid mailbox target is raised when Mailbox is left blank
