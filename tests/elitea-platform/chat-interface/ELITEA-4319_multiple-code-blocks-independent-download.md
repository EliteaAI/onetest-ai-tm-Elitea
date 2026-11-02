---
id: ELITEA-4319
title: "Download Works Independently for Each Code Block in a Multi-Code-Block Message"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment
- User has access to a Private project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Prompt | "Give me a small html page and a separate css stylesheet for it, as two distinct code blocks" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat` and open a direct chat conversation | Chat page loads |
| 2 | Send the prompt from the Test Data table | AI responds with a single message containing two distinct fenced code blocks (html and css) |
| 3 | Locate the Download icon on the first (html) code block's toolbar and click it | A file downloads |
| 4 | Open the downloaded file from step 3 | File content contains only the html code block's content, with no content from the css block |
| 5 | Locate the Download icon on the second (css) code block's toolbar and click it | A second, separate file downloads |
| 6 | Open the downloaded file from step 5 | File content contains only the css code block's content, with no content from the html block |
| 7 | Confirm that downloading one block did not alter, disable, or affect the Edit code/Copy code/Download controls of the other block | Both blocks' toolbars remain fully functional and independent after both downloads |

## Expected Final State

Two independently downloaded files exist, each containing exactly one of the two code blocks' content, with no cross-contamination between them.

## Pass/Fail Criteria

**Pass:**
- Each code block's Download produces a file containing only that block's content
- Neither block's controls are affected by interacting with the other block's controls

**Fail:**
- A downloaded file contains merged or cross-contaminated content from both blocks
- Interacting with one block's Download control disables or affects the other block's controls
