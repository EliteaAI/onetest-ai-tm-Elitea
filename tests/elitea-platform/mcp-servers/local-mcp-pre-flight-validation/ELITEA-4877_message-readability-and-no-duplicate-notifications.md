---
id: ELITEA-4877
title: "Verify message readability and no duplicate notifications"
priority: medium
type: functional
module: local-mcp
status: draft
execution_type: manual
tags: [r-2.0.9, feat:mcp-local, nfr:usability, nfr:validation]
requirements: [EliteaAI/elitea_issues#7070]
---

## Preconditions

- ELITEA MCP Client build containing #7070 is installed and the tray is running
- Windows desktop notifications are enabled
- Access to the tray log
- The issue's proposed message texts are available for comparison

## Test Data

| Field | Value |
|-------|-------|
| Long URL | A 200-character URL on an unreachable host |
| Failing configuration | Any invalid value, for example `auth_token`: `invalid-token-123` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set the long URL and select **Start MCP Server** | The notification is readable; the full text is in the log |
| 2 | With the failing configuration, select **Start MCP Server** several times quickly | Notifications are not duplicated endlessly |
| 3 | Compare the message wording with the issue's proposed texts | No typos; wording matches |
| 4 | Read the notification and tooltip text | No internal exception names or stack traces |

## Expected Final State

Error messages stay readable for long values, are not duplicated, and contain no internal technical details.

## Pass/Fail Criteria

**Pass:**
- Long messages are readable and the full text is in the log
- Repeated Start does not create an endless stream of notifications
- Wording matches the proposed text without typos
- No exception names or stack traces are shown

**Fail:**
- The notification is cut off unreadably
- Notifications multiply on repeated Start
- Internal exception names or stack traces appear
