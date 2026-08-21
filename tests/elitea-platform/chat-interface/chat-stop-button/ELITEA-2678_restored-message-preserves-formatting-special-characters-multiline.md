---
id: ELITEA-2678
title: "Restored message preserves formatting, special characters, and multi-line structure"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, issue:5000]
requirements: [EliteaAI/elitea_issues#5000]
---
# ELITEA-2678: Restored message preserves formatting, special characters, and multi-line structure

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the restored message in the input field maintains all original formatting, line breaks, special characters, and markdown syntax without loss or corruption.

## Preconditions

- User is logged in to `{{base_url}}`
- Regular chat interface is accessible

## Test Data

Test with the following message variations:

| Message Type | Test Data |
|--------------|-----------|
| Multi-line | "Line 1\nLine 2\nLine 3" |
| Special characters | "Test with @#$%^&*() symbols" |
| Code block | "\`\`\`python\nprint('hello')\n\`\`\`" |
| Markdown | "**Bold** and *italic* text" |
| URLs | "Check https://example.com for info" |
| Emojis | "Testing with 😀 🎉 ✅ emojis" |

## Steps

For **each message variation** in the Test Data table:

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open regular chat interface | Chat interface loads successfully |
| 2 | Type the test message from the current variation in the input field | Message appears in the input field with correct formatting |
| 3 | Click Send button | Message is sent and appears in the chat thread |
| 4 | Click Stop button during AI response processing | Stop button is clicked successfully |
| 5 | Check the input field for the restored text | Restored text appears in the input field |
| 6 | Compare the restored text character-by-character with the original | Text matches exactly: all characters, line breaks, special symbols, markdown syntax, URLs, and emojis are preserved |
| 7 | Verify no characters are escaped incorrectly (e.g., `\n` visible as literal text instead of line break) | All special characters and formatting render correctly |

## Expected Final State

Input field contains the original message text with 100% accuracy across all tested variations. No character loss, incorrect escaping, or formatting corruption.

## Pass/Fail Criteria

**Pass:**
- All message variations restore exactly as originally typed
- Line breaks, special characters, markdown, URLs, and emojis are preserved
- No incorrect escaping or character corruption

**Fail:**
- Any character is lost or altered
- Line breaks are lost or incorrectly escaped
- Special characters are corrupted or HTML-encoded
- Markdown syntax is broken
- Emojis are removed or replaced with placeholder characters
