---
id: ELITEA-0942
title: "Project Context Content Persists After Edit, Replace, and Clear"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, persistence, story:3395, unicode, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0942: Project Context Content Persists After Edit, Replace, and Clear

**Module:** Project Context · **Priority:** High · **Type:** Functional

**Objective:** Verify that Project Context content correctly persists after editing, replacing, clearing, and uploading Unicode/emoji content.

**Coverage:**
- Editing and saving replaces old content
- Clearing and saving results in empty context
- Unicode, emoji, and multilingual content saves without corruption

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Version A: `Version A content`
- Version B: `Version B content`
- Unicode .md content: `# 🌍 Unicode Test

中文: 人工智能
Russian: Привет
Arabic: مرحبا
Emoji: ✅🔴🟠`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set content to 'Version A content'. Save. | Content persists after reload. |
| 2 | Edit the content to 'Version B content'. Save. | 'Version B content' is shown after reload. 'Version A content' is gone. |
| 3 | Clear all content from the editor. Save. | Editor is empty after reload. Agent runs with no context injected. |
| 4 | Create a .md file with the following content: '# 🌍 Unicode Test\n\n中文: 人工智能\nRussian: Привет\nArabic: مرحبا\nEmoji: ✅🔴🟠'. Upload it and Save. | Content saves without corruption. All characters (emoji, Chinese, Russian, Arabic) display correctly in editor and Preview mode. |

## Expected Final State

Content saves without corruption. All characters (emoji, Chinese, Russian, Arabic) display correctly in editor and Preview mode.

## Pass/Fail Criteria

**Pass:**
- Each save correctly replaces previous content
- Empty save results in truly empty context
- Unicode/emoji content renders without corruption

**Fail:**
- Old content persists after saving new content
- Unicode characters appear as ? or boxes after save
