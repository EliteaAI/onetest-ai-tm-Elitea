---
id: ELITEA-1261
title: "SharePoint Indexing (Index data) Works with Both Auth Modes"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1261: SharePoint Indexing (Index data) Works with Both Auth Modes

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Index data tool (SharePoint document indexing into PgVector) works correctly with both App-only and Delegated auth modes.

**Coverage:**
- Index data tool indexes documents from SharePoint to PgVector store using App-only credentials
- Index data tool indexes documents using Delegated credentials
- Indexed content is retrievable via List collections and Search tools
- PgVector credential is required and validated

## Preconditions

- A valid elitea-pgvector credential configured in the system
- App-only and Delegated SharePoint credentials available
- SharePoint document library has at least 2 .txt or .docx files for indexing
- Toolkits with Index data and List collections tools enabled for both auth modes

## Test Data

- PgVector credential: `elitea-pgvector`
- Embedding model: `text-embedding-3-small`
- SharePoint folder to index: `Documents` (root document library)
- Expected collection name: auto-generated or `sp-test-collection`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open agent using the App-only SharePoint toolkit (with PgVector configured). Send: Index the SharePoint Documents folder into the vector store | Agent invokes Index data tool |
| 2 | Wait for indexing to complete. Observe agent response | Success message indicating N documents indexed. No errors |
| 3 | Send: List collections in the vector store | Collection created from SharePoint documents is listed |
| 4 | Open agent using the Delegated SharePoint toolkit (with PgVector). Send: Index the SharePoint Documents folder into the vector store | Agent invokes Index data tool via Graph API |
| 5 | Wait for indexing to complete | Success message. N documents indexed |
| 6 | Send: Search for test content in the SharePoint collection using the delegated toolkit | Relevant documents returned from the vector store |

## Expected Final State

Relevant documents returned from the vector store

## Pass/Fail Criteria

**Pass:**
- Indexing completes successfully for both App-only and Delegated modes
- Collections are created/updated in PgVector
- Indexed content is searchable
- No auth errors during indexing

**Fail:**
- Indexing fails with auth error for either mode
- Collection not created after indexing
- Indexed content is not searchable
