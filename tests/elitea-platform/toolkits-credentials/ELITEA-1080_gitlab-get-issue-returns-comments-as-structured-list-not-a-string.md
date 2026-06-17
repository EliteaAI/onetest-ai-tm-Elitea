---
id: ELITEA-1080
title: "GitLab - get_issue Returns Comments as Structured List, Not a String"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [r-2.0.2]
requirements: [EliteaAI/elitea_issues#4055]
---
# ELITEA-1080: GitLab - get_issue Returns Comments as Structured List, Not a String

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after the fix (removing `str()` wrapper on line 348 of `api_wrapper.py`), the `comments` field in the `get_issue` tool output is a proper JSON array, not a string.

**Coverage:**
- `comments` field type is array (not string) in raw tool output
- Array structure survives all ELITEA execution contexts (Toolkit Test Settings, Chat, Agent)
- Previously broken: `"[{'body': '...', 'user': '...'}]"` (string)
- Fixed: `[{"body": "...", "user": "..."}]` (array)

## Preconditions

- Logged into {{base_url}} (stage environment)
- GitLab toolkit configured with valid Personal Access Token credentials
- `get_issue` tool enabled on the toolkit
- Target issue (e.g., issue #1 in test repo) has at least 2 comments with distinct bodies

## Test Data

- Toolkit: GitLab toolkit connected to test repository
- Issue number: 1 (or any test issue with ≥2 comments)
- Expected `comments` type: JSON array

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the GitLab toolkit → Toolkit Test Settings panel | Toolkit Test Settings panel opens and lists available tools |
| 2 | Select `get_issue` tool and enter `issue_number: 1` | Tool invocation form is displayed with issue_number field |
| 3 | Click Run / Execute | Tool executes and raw JSON output is displayed |
| 4 | Inspect the `comments` field in the output | `comments` value is a JSON array [{...}, {...}] — NOT a string "[{...}]" |
| 5 | Verify there is no surrounding pair of double quotes wrapping the array | The field is "comments": [...], not "comments": "[...]" |
| 6 | Repeat via ELITEA Chat: send 'Get issue #1 from [repo]' using an agent with the GitLab toolkit | Agent response contains comments presented as list items, not a raw string dump |

## Expected Final State

Agent response contains comments presented as list items, not a raw string dump

## Pass/Fail Criteria

**Pass:**
- `comments` field is a JSON array with ≥1 object
- No string-type wrapping of the array
- Tool executes without error in Toolkit Test Settings
- Agent response correctly lists comment content

**Fail:**
- `comments` is a string value, e.g. "[{'body': '...'}]"
- Tool throws a TypeError or validation error
- Agent cannot process the comments field
