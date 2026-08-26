---
id: ELITEA-2828
title: "Source-Appropriate Item Terminology in Summaries"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:indexing-summary, terminology, toolkits]
requirements: [EL-6229]
---
# ELITEA-2828: Source-Appropriate Item Terminology in Summaries

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that indexing summaries use contextually correct terminology based on the toolkit/source type.

**Coverage:**
- Artifacts toolkit uses "files" terminology
- Confluence toolkit uses "pages" terminology
- Jira toolkit uses "issues" terminology
- GitHub toolkit uses appropriate entity names
- Generic "documents" is NOT used when specific term available

## Preconditions

- Logged in to {{base_url}}
- Access to multiple toolkit types with completed indexes:
  - Artifacts toolkit with index
  - Confluence toolkit with index (if available)
  - Jira toolkit with index (if available)
  - GitHub toolkit with index (if available)

## Test Data

| Toolkit Type | Expected Terminology |
|--------------|---------------------|
| Artifacts | "files" or "documents" |
| Confluence | "pages" or "attachments" |
| Jira | "issues", "comments", or "attachments" |
| GitHub | "repositories", "issues", "pull requests", or "files" |
| SharePoint | "files", "pages", or "documents" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes. | Toolkits list displays. |
| 2 | Select an Artifacts toolkit → open Index History. | Index History displays. |
| 3 | View the summary of a recent indexing event. | Summary shows terminology. |
| 4 | Verify the summary uses "files" (not generic "documents"). | "N files indexed successfully" or similar. |
| 5 | If Confluence toolkit available: open its Index History. | Confluence Index History displays. |
| 6 | Verify the summary uses "pages" or "attachments". | Appropriate Confluence terminology used. |
| 7 | If Jira toolkit available: open its Index History. | Jira Index History displays. |
| 8 | Verify the summary uses "issues", "comments", or "attachments". | Appropriate Jira terminology used. |
| 9 | For each toolkit checked, verify NO generic "documents" when specific term fits. | Specific terminology used throughout. |

## Expected Final State

Each toolkit type displays indexing summaries using source-appropriate item terminology.

## Pass/Fail Criteria

**Pass:**
- Artifacts uses "files"
- Confluence uses "pages"/"attachments"
- Jira uses "issues"/"comments"/"attachments"
- GitHub uses appropriate entity names
- Generic "documents" avoided when specific term available

**Fail:**
- Generic "documents" used for Artifacts
- Wrong terminology for toolkit type
- Inconsistent terminology within same toolkit
- Technical terms used instead of user-friendly labels
