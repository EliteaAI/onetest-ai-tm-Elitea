---
id: ELITEA-4326
title: "Download Handles Edge-Case Code Block Content: Large Block, Empty Block, Special Characters/Unicode/Mixed Line Endings"
priority: medium
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

| Case | Prompt / setup |
|---|---|
| Very large code block | "Give me a very long json array with at least 2000 lines of sample data, as one code block" |
| Empty code block | A message/response containing a fenced code block with no content between the fences |
| Special characters/Unicode | "Give me a code comment block containing emoji, accented characters (e, u, n with diacritics), and non-Latin text (e.g. Chinese or Cyrillic), inside a code block" |
| Mixed line endings | A code block whose source content mixes CRLF and LF line endings (may require a crafted/injected response or an uploaded-then-echoed snippet if the AI cannot reliably produce this) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the "very large code block" prompt and wait for the response | AI responds with a large fenced code block (approx. 2000+ lines); Download icon is present and not disabled due to size |
| 2 | Click Download on the large code block | File downloads completely (no truncation, no timeout/error) with content matching the full block |
| 3 | Produce or locate a response containing an empty code block (e.g. ask the AI to show an empty code block, or construct one via a minimal prompt) | An empty fenced code block renders with its toolbar, including a Download icon |
| 4 | Click Download on the empty code block | Download completes without error, producing a valid (zero-byte or near-empty) file rather than crashing or silently failing |
| 5 | Send the "special characters/Unicode" prompt and wait for the response | AI responds with a code block containing emoji, accented characters, and non-Latin script |
| 6 | Click Download on this code block and open the downloaded file in a text editor with UTF-8 encoding | All special characters, accented letters, and non-Latin text are preserved correctly and are not corrupted, mangled, or replaced with mojibake/placeholder characters |
| 7 | If a mixed-line-ending code block can be produced or observed, click Download on it and inspect the file's line endings (e.g. via a hex/text editor that shows CRLF vs LF) | The downloaded file preserves the code block's content faithfully; line endings are handled consistently without corrupting the visible text or merging/splitting lines incorrectly |

## Expected Final State

Downloads succeed and preserve content integrity for all tested edge cases: a very large block, an empty block, a block with special characters/Unicode, and a block with mixed line endings.

## Pass/Fail Criteria

**Pass:**
- Large code block downloads completely and matches the full displayed content
- Empty code block download completes without error and produces a valid (empty/near-empty) file
- Special characters and Unicode are preserved correctly in the downloaded file
- Mixed line endings do not corrupt or visibly alter the downloaded content

**Fail:**
- Large code block download times out, truncates, or errors
- Empty code block causes a crash, error toast, or no response when Download is clicked
- Special characters/Unicode are corrupted, mangled, or replaced with placeholder characters in the downloaded file
- Mixed line endings cause visible corruption or data loss in the downloaded file
