---
id: ELITEA-4549
title: "Platform credential and injected toolkit settings are never exposed to non-public-admin users"
priority: critical
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- A viewer-only user account exists in a non-public (personal/private) project
- Browser devtools (Network/WS tabs) are available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Chat prompt | A query that triggers a web search |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the viewer-only user in a personal/non-public project; enable Web Search and send the test prompt | Response returns normally |
| 2 | Capture all chat API responses and websocket events during the exchange via devtools | Payloads are captured |
| 3 | Inspect captured payloads for the Tavily API key/credential value or the injected toolkit's fully expanded configuration | None present; credentials appear only as masked/reference values, if at all |
| 4 | Open Run History / trace view for this run as the same non-public-admin user | No credential or expanded toolkit settings for the injected "Web Search" toolkit are visible |

## Expected Final State

No credential or expanded toolkit configuration is observable to the non-public-admin viewer through any inspected surface.

## Pass/Fail Criteria

**Pass:**
- No secret or expanded setting appears in any captured payload or trace view

**Fail:**
- The Tavily credential value or the injected toolkit's full settings appear anywhere in the inspected surfaces
