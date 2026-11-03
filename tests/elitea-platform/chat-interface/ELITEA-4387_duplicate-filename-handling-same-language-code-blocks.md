---
id: ELITEA-4387
title: "Duplicate Filename Handling When Downloading Multiple Code Blocks of the Same Language"
priority: high
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
- Downloaded filename for a code block is a fixed pattern (e.g. `code.<ext>`) rather than one derived from message/conversation identity (per implementation notes), so repeated downloads of same-language blocks are expected to collide on name

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Prompt 1 (json block A) | "Give me a sample json config object for a database connection" |
| Prompt 2 (json block B, different message) | "Give me a different sample json object representing a user profile" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat` and open a direct chat conversation | Chat page loads with message input available |
| 2 | Send Prompt 1 and wait for the response | AI responds with a message containing a fenced json code block and a Download icon in its toolbar |
| 3 | Click the Download icon on the Prompt 1 code block and note the downloaded filename in the browser's downloads folder | A file downloads (e.g. `code.json`) |
| 4 | Send Prompt 2 (a separate message) and wait for the response | AI responds with a second message containing a distinct fenced json code block and its own Download icon |
| 5 | Click the Download icon on the Prompt 2 code block | A second download is initiated; the browser either auto-renames the file (e.g. `code (1).json`) or prompts/overwrites, depending on browser/download-manager behavior |
| 6 | Inspect both files now present in the downloads folder | Two files exist (not one overwritten by the other, unless the user's browser is configured to always overwrite) |
| 7 | Open each downloaded file and compare its content against its respective source code block (Prompt 1's json vs Prompt 2's json) | Each file's content corresponds correctly to its own source code block; no file contains the wrong block's content, and no data loss occurred |
| 8 | Repeat steps 2-7 using a third same-language (json) code block from a third message | The third download also completes correctly, auto-renamed or otherwise distinguished, with correct content and no silent overwrite of either prior file's content |

## Expected Final State

Multiple downloads of same-language code blocks from different messages all complete successfully, and each resulting file's content corresponds correctly and exclusively to its own source code block, regardless of how the browser names/renames colliding filenames.

## Pass/Fail Criteria

**Pass:**
- Each download of a same-language code block completes without error
- No downloaded file's content is silently replaced with the wrong block's content
- The browser's standard filename-collision handling (auto-rename, overwrite prompt, etc.) behaves predictably and does not cause data loss across repeated same-language downloads

**Fail:**
- A later download overwrites an earlier file with the wrong content without any indication to the user
- Any download fails, errors, or produces a corrupted/empty file due to the filename collision
- A downloaded file's content does not match its own source code block after a filename collision
