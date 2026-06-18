---
id: ELITEA-0947
title: "Project Context .md File Import Is Rejected If Content Exceeds 2500 Characters"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, file-upload, char-limit, story:3395, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0947: Project Context .md File Import Is Rejected If Content Exceeds 2500 Characters

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that importing a .md file enforces the 2500-character limit — files within the limit are accepted; files exceeding it are rejected without clearing existing editor content.

**Coverage:**
- File ≤2500 chars is accepted
- File with 2501 chars is rejected with clear error
- Far oversized file is rejected
- Editor content is unchanged after rejected import

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Valid file: a .md file with a short project overview, e.g. '# Project Alpha

Stack: Node.js, React.
Rule: Always cite sources.' (well under 2500 chars)
- Boundary file: a .md file with exactly 2500 characters of Markdown text
- Over-limit file: a .md file with 2501 characters
- Oversized file: a .md file with several thousand characters of content

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Upload a .md file containing a short project overview (well under 2500 chars). | File accepted. Content loads into the editor. No error shown. |
| 2 | Save the content. | Save succeeds. |
| 3 | Upload a .md file with exactly 2501 characters of content. | File rejected. A clear error message is shown (e.g. 'Content exceeds the 2500 character limit'). Editor content is unchanged. |
| 4 | Upload a .md file with several thousand characters. | File rejected with the same error. No silent truncation occurs. Editor content is unchanged. |

## Expected Final State

File rejected with the same error. No silent truncation occurs. Editor content is unchanged.

## Pass/Fail Criteria

**Pass:**
- File within limit is accepted and loads into editor
- File over limit is rejected with clear error
- Editor content unchanged after rejected import
- No silent truncation

**Fail:**
- Oversized file is silently truncated and accepted
- Error message is missing or unclear
- Editor content cleared on rejected import
