---
id: ELITEA-4914
title: "Verify existing deep links still open the correct pages"
priority: medium
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562, EliteaAI/elitea_issues#7560]
---
# ELITEA-4914: Verify existing deep links still open the correct pages


## Preconditions

- User is logged in to `{{base_url}}` with access to all sections
- An existing chat URL and an existing agent URL are known

## Test Data

Routes come from `EliteaUI/src/routes.js`; check the exact project prefix on dev before running.

| # | Deep link | Expected page | Expected sidebar highlight |
|---|-----------|---------------|---------------------------|
| 1 | `{{base_url}}/app/<project>/chat` | Chat page | None of the Explore items |
| 2 | Existing chat URL | That chat | That chat in history |
| 3 | `{{base_url}}/app/<project>/agents` | Agents | Explore + Agents |
| 4 | `{{base_url}}/app/<project>/pipelines` | Pipelines | Explore + Pipelines |
| 5 | `{{base_url}}/app/<project>/skills` | Skills | Explore + Skills |
| 6 | `{{base_url}}/app/<project>/toolkits` | Toolkits & Indexes | Explore + Toolkits & Indexes |
| 7 | `{{base_url}}/app/<project>/mcps` | MCPs | Explore + MCPs |
| 8 | `{{base_url}}/app/<project>/apps` | Applications | Explore + Applications |
| 9 | `{{base_url}}/app/<project>/credentials` | Credentials | Explore + Credentials |
| 10 | `{{base_url}}/app/<project>/elitea-catalog` | The page agreed for the removed Catalog item (catalog or Discover), no 404 | As agreed |
| 11 | Existing agent URL | That agent's page | Explore + Agents |
| 12 | `{{base_url}}/app/<project>/artifacts` | Artifacts | Artifacts |
| 13 | `{{base_url}}/app/<project>/settings` | Settings | Settings; no Explore item selected |
| 14 | `{{base_url}}/app/<project>/apps/catalog` | Applications Discover/Catalog tab | Explore + Applications |
| 15 | `{{base_url}}/app/<project>/agents/<tab>/<agentId>` with tab `all` or `favorites` as on dev | The agent detail page | Explore + Agents |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Paste the deep link from the Test Data row into a new tab | The page loads without errors |
| 2 | Check the opened page | It matches "Expected page" |
| 3 | Check the sidebar | The highlight matches "Expected sidebar highlight", and the Chats history is loaded |
| 4 | Repeat for every row | All rows pass |

## Expected Final State

Bookmarked and shared URLs keep working after the menu change.

## Pass/Fail Criteria

**Pass:**
- Every link opens its page with the correct sidebar state

**Fail:**
- Any link shows a 404 or blank page, opens the wrong page, or has the wrong highlight
