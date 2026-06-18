---
id: ELITEA-0936
title: "Character Count Is Consistent Between File Import and Editor Input"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, file-upload, char-limit, story:3395, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395, EliteaAI/elitea_issues#5322]
---
# ELITEA-0936: Character Count Is Consistent Between File Import and Editor Input

**Module:** Project Context · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that character counting is consistent between manual editor input and .md file import — the same content that fits in the editor should also import successfully.

**Coverage:**
- Content within limit in editor also accepted on import
- Counter value after import is approximately the same as before export
- Minor edits after import change counter by expected amount

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type content in the editor until the counter shows '1 character left'. Note the exact count shown. | Counter shows 1 / 2500. |
| 2 | Save this content locally as a .md file. | File saved. |
| 3 | Upload the saved .md file via the Upload button. | Import succeeds. The same content that fit in the editor is also accepted on import. |
| 4 | Check the character counter immediately after import. | Counter shows approximately the same remaining chars as before (close to 1), not a significantly different number. |
| 5 | Add one character to the content in the editor. | Counter changes by 1 (e.g. from 1 to 0). Does NOT jump by 40–50 characters. |

## Expected Final State

Counter changes by 1 (e.g. from 1 to 0). Does NOT jump by 40–50 characters.

## Pass/Fail Criteria

**Pass:**
- File containing editor-acceptable content imports without rejection
- Counter after import matches expected remaining chars (within ~5 chars)
- Adding 1 char changes counter by 1

**Fail:**
- File rejected even though same content fit in editor
- Counter jumps by 40+ chars after single character edit post-import
- Counting logic differs between import and editor
