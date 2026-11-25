---
id: ELITEA-4874
title: "Verify raw response text is never shown to the user"
priority: high
type: functional
module: local-mcp
status: draft
execution_type: manual
tags: [r-2.0.9, feat:mcp-local, nfr:usability, nfr:validation]
requirements: [EliteaAI/elitea_issues#7070]
---

## Preconditions

- ELITEA MCP Client build containing #7070 is installed and the tray is runnable
- A way to reproduce an HTML error page, 401, 404 and 5xx responses
- Access to the tray log and the console output

## Test Data

| Failure | Setup |
|---------|-------|
| HTML error page | `https://example.com` as deployment URL |
| 401 | Invalid token |
| 404 | Non-existent project or path |
| 5xx | A server or proxy returning a 5xx response |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Reproduce each failure in Test Data | Each failure is reported |
| 2 | Check the tray notification, tooltip and console for HTML tags, JSON bodies or long text | Only a status code and a short message are shown |
| 3 | With Debug Logging off, open the log | It contains no response body |
| 4 | Turn Debug Logging on and repeat the failures | Response details appear in the log at DEBUG level |
| 5 | Search all logs for the token, `env` and `headers` values | They are masked as `****` |

## Expected Final State

Users see a status code and a short message. Response details appear only in the DEBUG log, and secrets are always masked.

## Pass/Fail Criteria

**Pass:**
- No HTML, JSON body or long raw text in the tray, tooltip or console
- No response body in the log with Debug Logging off
- Details appear with Debug Logging on
- Token, `env` and `headers` values are masked

**Fail:**
- Raw response text reaches the user
- Secrets appear unmasked in any log
