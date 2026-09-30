---
id: ELITEA-3511
title: "Popup-Blocked and Auth-Metadata-Unavailable States Are Handled"
priority: high
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3511: Popup-Blocked and Auth-Metadata-Unavailable States Are Handled

**Module:** Outlook Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify the OAuth modal degrades gracefully when the browser blocks the popup, or when the discovery endpoint's metadata cannot be fetched.

## Preconditions

- Browser popup blocking can be toggled

## Test Data

- Invalid/unreachable OAuth Discovery Endpoint, e.g. `https://login.microsoftonline.com/00000000-non-existent-tenant`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable popup blocking in the browser | Popup blocking active |
| 2 | Click "Authorize" in the `McpAuthModal` | Modal shows "Popup blocked. Please allow popups for this site and try again." and does not hang |
| 3 | Re-run Test Connection with an invalid/unreachable `oauth_discovery_endpoint` | Request is processed |
| 4 | Observe the modal | Modal shows the `mcp-auth-metadata-unavailable` error state instead of a broken authorize form |

## Expected Final State

Both failure modes are shown as clear, handled UI states rather than a hung or broken modal.

## Pass/Fail Criteria

**Pass:**
- Popup-blocked case shows the documented message without hanging
- Unreachable discovery endpoint shows the `mcp-auth-metadata-unavailable` state

**Fail:**
- Modal hangs indefinitely in either case
- A broken/blank authorize form is shown instead of a handled error state
