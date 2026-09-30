---
id: ELITEA-3535
title: "Re-Authenticating the Credential Does Not Break an Existing Toolkit or Other Toolkits"
priority: high
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3535: Re-Authenticating the Credential Does Not Break an Existing Toolkit or Other Toolkits

**Module:** Outlook Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify re-running the OAuth flow on a credential (e.g. after ELITEA-3506's re-authorization) does not break existing toolkits already linked to it, nor a second toolkit sharing the same credential.

## Preconditions

- One authorized Outlook credential
- Two toolkits both linked to that same credential (e.g. `outlook-toolkit-e2e` and a second toolkit `outlook-toolkit-second`)

## Test Data

- Credential shared by both toolkits

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm both toolkits work (invoke a tool on each) | Both succeed |
| 2 | Re-authenticate the shared credential (repeat the OAuth login flow, e.g. after a forced token invalidation) | Credential shows logged in again with a fresh token |
| 3 | Re-invoke a tool on the first toolkit | Succeeds using the refreshed token |
| 4 | Re-invoke a tool on the second toolkit | Also succeeds using the refreshed token, with no reconfiguration needed |

## Expected Final State

Both toolkits continue to function correctly after the credential is re-authenticated.

## Pass/Fail Criteria

**Pass:**
- Both toolkits work before and after re-authentication with no reconfiguration

**Fail:**
- Either toolkit breaks, requires re-linking, or fails after the credential is re-authenticated
