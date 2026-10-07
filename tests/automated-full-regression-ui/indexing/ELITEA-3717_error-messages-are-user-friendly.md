---
id: ELITEA-3717
title: "Verify error messages are user-friendly"
priority: critical
type: functional
module: indexes
status: draft
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has toolkit configurations that will trigger various error scenarios

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Error scenarios | Invalid credentials, Rate limit, Source unavailable, Permission denied |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger indexing with invalid credentials | Indexing fails |
| 2 | View error message displayed | Error message is user-friendly |
| 3 | Verify message content | Message explains the issue in plain language (e.g., "Authentication failed. Please check your credentials.") |
| 4 | Verify no raw technical errors shown | No stack traces, HTTP codes, or driver-level text visible |

## Expected Final State

Error messages are displayed in user-friendly language without technical jargon.

## Pass/Fail Criteria

**Pass:**
- Error message is understandable by non-technical users
- Message provides actionable guidance
- No raw exception text, HTTP status codes, or stack traces shown

**Fail:**
- Error shows raw technical text (e.g., "psycopg2.OperationalError", "HTTPError 503")
- Message is unclear or generic (e.g., "An error occurred")
