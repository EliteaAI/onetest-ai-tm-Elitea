---
id: ELITEA-1228
title: "[EliteaAI/elitea_issues#4660] SharePoint — Proactive Token Refresh at 75% Lifetime (Rate-Limited to 60s)"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [proactive-refresh, feat:credentials, int:sharepoint, feat:toolkits, issue:4660, int:oauth, r-2.0.3]
requirements: [4660]
---
# ELITEA-1228: [EliteaAI/elitea_issues#4660] SharePoint — Proactive Token Refresh at 75% Lifetime (Rate-Limited to 60s)

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the proactive refresh mechanism: when a token has exceeded 75% of its lifetime AND at least 60 seconds have passed since the last refresh check (`REFRESH_CHECK_INTERVAL_MS`), `getAllTokens()` detects the near-expiry condition, queues the token for refresh, and fires a background `POST /mcp/oauth` with `grant_type=refresh_token` — before the access token actually expires.

## Preconditions

SharePoint toolkit authenticated
`issued_at` and `expires_at` are stored in the sessionStorage token entry
Token lifetime is a known value (e.g., Azure AD default 3600 seconds = 1 hour)
Browser DevTools Network tab open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Authenticate to SharePoint and note `issued_at` and `expires_at` in sessionStorage. Calculate the 75% threshold: `threshold = issued_at + (expires_at - issued_at) * 0.75`. | Token timestamps visible. For a 1-hour token: proactive refresh fires after ~45 minutes. |
| 2 | Simulate or wait until current time is past the 75% threshold (e.g., manually set `issued_at` in sessionStorage to a value 46+ minutes in the past while keeping a valid `access_token`). | Token is now past 75% lifetime. Access token is still technically valid. |
| 3 | Send a chat message to a SharePoint-enabled agent. Monitor Network tab for a POST to `/mcp/oauth` or similar refresh endpoint. | A background refresh request fires (fire-and-forget). Request payload contains `grant_type=refresh_token`. The main SharePoint tool call also completes successfully. |
| 4 | Send another chat message immediately (within 60 seconds of the previous one). | NO second refresh request is fired. The 60-second rate limit prevents repeated checks within the same window. |
| 5 | Wait 60+ seconds and send another message. | If still past 75% threshold, another proactive refresh fires. Rate-limited check window has reset. |

## Expected Final State

If still past 75% threshold, another proactive refresh fires. Rate-limited check window has reset.

## Pass/Fail Criteria

Background POST /mcp/oauth with grant_type=refresh_token observed in Network tab when at 75%+ lifetime
Refresh fires at most once per 60-second window (not on every message)
SessionStorage updated with new access_token after proactive refresh
Access token is still valid (not null) before and after the proactive refresh
