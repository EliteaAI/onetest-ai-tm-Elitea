---
id: ELITEA-4870
title: "Verify each pre-flight scenario shows its own specific message"
priority: high
type: functional
module: local-mcp
status: draft
execution_type: manual
tags: [r-2.0.9, feat:mcp-local, nfr:usability, nfr:validation]
requirements: [EliteaAI/elitea_issues#7070]
---

## Preconditions

- ELITEA MCP Client build containing #7070 is installed; `elitea-mcp tray`, `serve` and `run` are available
- A valid baseline configuration (URL, token, project ID)
- A project with no agents tagged `mcp`, and a project the user is not a member of
- The issue's table of proposed messages is available for comparison

## Test Data

| Scenario | Setup |
|----------|-------|
| URL looks like a UI link | `{{base_url}}/app/13/mcp` |
| Host unreachable (DNS) | `https://does-not-exist.invalid` |
| Host unreachable (refused) | `http://localhost:9` |
| Host unreachable (timeout) | Blackholed address |
| Not an ELITEA API | `https://example.com` |
| Token invalid or expired | Invalid or expired token |
| No project access | Valid token, project the user is not a member of |
| Project does not exist | `project_id: 999999` |
| `project_id` not set | Key removed |
| `run`: no agents tagged `mcp` | Project without `mcp`-tagged agents |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Reproduce the first scenario and record the tray notification, tooltip, first tray menu line, console line and log line | Each place shows a message for this scenario |
| 2 | Repeat step 1 for every scenario in Test Data (use `run` for the last one) | Each scenario produces a message |
| 3 | Compare each message with the issue's proposed message | Wording names the host or URL, the cause and what to do |
| 4 | Compare all messages with each other | No two different scenarios produce the same message |

## Expected Final State

Each pre-flight scenario has its own message, consistent across the tray, console and log.

## Pass/Fail Criteria

**Pass:**
- All 10 scenarios produce a message that matches the issue's proposed wording
- No two scenarios share the same message
- Tray and console/log texts agree

**Fail:**
- Two scenarios show the same message
- A message lacks the cause or the action to take
- The tray and the console/log differ
