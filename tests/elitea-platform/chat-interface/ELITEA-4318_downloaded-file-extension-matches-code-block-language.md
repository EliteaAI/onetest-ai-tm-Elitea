---
id: ELITEA-4318
title: "Downloaded Chat Code Block File Has Correct Name and Extension per Language"
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

| Fenced language tag | Expected downloaded file extension |
|---|---|
| html | .html |
| css | .css |
| json | .json |
| xml | .xml |
| txt | .txt |
| (no language tag specified) | a sensible default extension (e.g. .txt) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat` and open a direct chat conversation | Chat page loads |
| 2 | Send a prompt that produces an AI response containing a code block fenced with the "html" language tag | AI responds with a rendered html code block and a Download icon in its toolbar |
| 3 | Click Download and inspect the downloaded file's name and extension | Downloaded filename has the `.html` extension |
| 4 | Repeat steps 2-3 for each remaining row of the Test Data table (css, json, xml, txt, no-tag) | Each downloaded file has the extension listed in the Test Data table for its corresponding language |
| 5 | For the "no language tag" case specifically, confirm the download still completes successfully | A file downloads successfully with a default/sensible extension; no error is thrown |

## Expected Final State

Each of the six tested code block variants has produced a downloaded file whose extension correctly corresponds to its fenced language (or a sensible default for untagged blocks).

## Pass/Fail Criteria

**Pass:**
- Each language's downloaded file extension matches the mapping defined in the Test Data table
- The no-language-tag case downloads successfully with a reasonable default extension

**Fail:**
- Any language downloads with an incorrect or generic extension that does not reflect its content type
- The no-language-tag case fails to download or throws an error
