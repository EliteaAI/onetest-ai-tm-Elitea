---
id: ELITEA-4539
title: "Verify api_base_url is not present as a configurable field on either the credential or the toolkit"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- User is logged in to `{{base_url}}`

## Test Data

| Form | Fields to inspect |
|------|---------------------|
| Tavily credential create/edit form | All visible fields |
| Tavily toolkit create/edit form | All visible fields, including any "Show more"/expanded section |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Tavily credential creation/edit form | No field resembling "Base URL", "API Base URL", "Endpoint", or similar exists |
| 2 | Open the Tavily toolkit creation/edit form, including any expanded/"Show more" section | Same absence confirmed |

## Expected Final State

No user-facing way exists to set a custom base URL for Tavily.

## Pass/Fail Criteria

**Pass:**
- Neither form exposes any base-URL-like field anywhere, including expanded sections

**Fail:**
- Any base-URL-like field is present on either form
