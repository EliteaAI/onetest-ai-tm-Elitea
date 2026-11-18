---
id: ELITEA-4737
title: "Instructions Preview renders edge-case and large Markdown content safely"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4737: Instructions Preview renders edge-case and large Markdown content safely

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that Instructions Preview handles unusual, unsafe and large content without layout breaks, script execution or freezes.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- Agents "QA-7377 EdgeCases", "QA-7377 Empty" and "QA-7377 Large" (about 40,000 characters) exist.

---

## Test Data

| # | Instructions content (set in Edit on "QA-7377 EdgeCases" unless another agent is named) | Expected in Preview |
|---|---|---|
| 1 | Empty ("QA-7377 Empty") | A sensible empty state or placeholder. No broken box |
| 2 | Plain text with no Markdown and many blank lines | Readable paragraphs. No layout break |
| 3 | Only a `---` line, or a body with `---` horizontal rules | Shown as a horizontal rule. Not treated as frontmatter, and no content is hidden |
| 4 | `<script>alert(1)</script>` and `<img src=x onerror=alert(1)>` | No alert appears and no script runs. The content is escaped or removed |
| 5 | A 500-character URL or word with no breaks | Wraps or scrolls inside the section. No horizontal page overflow |
| 6 | Mermaid block, lists nested 5 levels deep, a 15-column table | Each renders (or the Mermaid block shows as code) without breaking the layout. The wide table scrolls inside its container |
| 7 | Cyrillic, CJK and emoji text (for example, `Привет 你好 🎉`) | All characters are shown correctly |
| 8 | "QA-7377 Large" (about 40,000 characters) | Renders and scrolls smoothly. Switching modes takes less than about 2 seconds |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent for the first row in the Test Data table. In Edit, set the content (if needed), then switch to Preview | The result matches the "Expected in Preview" column |
| 2 | Scroll through the content | Long content scrolls inside the section or page and does not overlap WELCOME MESSAGE or the chat panel |
| 3 | Check the browser console | No errors and no script output |
| 4 | Repeat steps 1–3 for every other row in the Test Data table | Every row passes |
| 5 | Discard the changes on "QA-7377 EdgeCases" | The agent returns to its saved content |

---

## Expected Final State

The test agents are unchanged.

---

## Pass/Fail Criteria

**Pass:**
- Every edge-case input renders safely and readably, with no script execution and no freezes.

**Fail:**
- A script runs, the layout breaks or overlaps, content is hidden or treated as frontmatter, or large content freezes the UI.

---

## Notes

- Related XSS coverage in other areas: ELITEA-2725 (artifacts), ELITEA-0934 (project context).
