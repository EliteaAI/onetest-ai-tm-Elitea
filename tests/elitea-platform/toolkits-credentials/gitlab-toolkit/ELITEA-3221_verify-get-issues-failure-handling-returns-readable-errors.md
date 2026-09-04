---
id: ELITEA-3221
title: "Verify get_issues failure handling returns readable errors instead of crashing"
priority: critical
type: functional
module: gitlab-toolkit
status: draft
execution_type: manual
tags: [r-2.0.6, int:gitlab]
requirements: [EliteaAI/elitea_issues#6213]
---

## Preconditions

- GitLab toolkit and GitLab Org toolkit configured
- A second credential/repository combination without access, for the authorization-error scenario

## Test Data

| Field | Value |
|-------|-------|
| `state` (invalid) | `bogus` |
| Repository/token combination | Valid repo with a token lacking access |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Invoke `get_issues` with `state=bogus` (an invalid/unsupported value) on the plain GitLab toolkit | The resulting GitLab API rejection is caught and surfaced as a readable tool error (`ToolException`), not a raw stack trace |
| 2 | Repeat the same invalid `state` call on the GitLab Org toolkit | The broader try/except (which also wraps repository resolution) still returns a readable error rather than swallowing it silently or crashing the agent turn |
| 3 | Point the toolkit at a repository/token combination without access and invoke `get_issues` on the plain GitLab toolkit | A clear authorization/error message is returned |
| 4 | Repeat step 3 on the GitLab Org toolkit | A clear authorization/error message is returned |

## Expected Final State

Both toolkits surface GitLab API errors and access failures as readable tool errors, with no unhandled crashes or silent failures.

## Pass/Fail Criteria

**Pass:**
- Invalid `state` produces a readable `ToolException` message on both toolkits
- Unauthorized access produces a clear, readable authorization error on both toolkits
- The agent turn does not crash in any scenario

**Fail:**
- A raw stack trace or unhandled exception is surfaced to the user
- The error is silently swallowed with no feedback
- The agent turn crashes
