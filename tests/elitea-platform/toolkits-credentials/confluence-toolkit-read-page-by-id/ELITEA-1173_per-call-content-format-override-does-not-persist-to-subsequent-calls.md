---
id: ELITEA-1173
title: "Per-call content_format override does not persist to subsequent calls"
priority: high
type: functional
module: confluence-toolkit-read-page-by-id
status: ready
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:3886, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3886]
---
# ELITEA-1173: Per-call content_format override does not persist to subsequent calls

**Module:** Confluence Toolkit Read Page By Id · **Priority:** High · **Type:** Functional

**Objective:** Verify that specifying content_format on a single call does not mutate the toolkit-level default — the next call without content_format must use the toolkit default, not the previously overridden value.

**Coverage:**
- Per-call override is scoped to that call only
- self.content_format not mutated after override call
- Subsequent call without content_format reverts to toolkit default

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Confluence toolkit configured with toolkit-level content_format set to view
- Page IDs 43679747 exists

## Test Data

- Page ID: 43679747
- Call 1 content_format: storage
- Call 2 content_format: not provided

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call read_page_by_id with page_id=43679747 and content_format=storage | Response body contains XHTML storage XML — confirms storage format was used |
| 2 | Immediately call read_page_by_id again with page_id=43679747 and no content_format parameter | Tool call is accepted without error |
| 3 | Inspect the response from step 2 | Response body is in view (HTML) format — the toolkit-level default — not in storage format |
| 4 | Compare responses from step 1 and step 2 | Step 1 contains raw storage XHTML; step 2 contains rendered view HTML — confirming the override did not persist |

## Expected Final State

Step 1 contains raw storage XHTML; step 2 contains rendered view HTML — confirming the override did not persist

## Pass/Fail Criteria

**Pass:**
- Call 1 returns storage XML
- Call 2 returns view HTML (toolkit default)
- Override did not leak into call 2

**Fail:**
- Call 2 returns storage XML instead of view HTML
- Override persisted across calls
