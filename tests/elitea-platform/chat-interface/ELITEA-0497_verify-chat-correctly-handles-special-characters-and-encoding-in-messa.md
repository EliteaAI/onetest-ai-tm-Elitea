---
id: ELITEA-0497
title: "Verify chat correctly handles special characters and encoding in messages"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat]
requirements: []
---
# ELITEA-0497: Verify chat correctly handles special characters and encoding in messages

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Chat messages containing special characters (HTML entities, unicode, angle brackets, ampersands, quotes) are not rendered correctly due to text encoding/escaping issues. Characters may be double-escaped, stripped, or displayed as raw HTML entities instead of their intended representation.

## Preconditions

User is logged into Elitea platform
A conversation exists or can be created
User has access to Chat functionality

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat page and open an existing conversation or create a new one | Chat page loads with message input area visible and ready for input |
| 2 | Send a message containing HTML angle brackets: 'Test <div> tag and <script> content' | Message is displayed exactly as typed with angle brackets visible, not interpreted as HTML or stripped |
| 3 | Send a message containing ampersand entities: 'Price is $5 & tax is 10% — total: $5.50' | Ampersand and special dash characters display correctly without being double-escaped (no visible &amp; or &mdash;) |
| 4 | Send a message containing unicode characters: 'Emojis: 🎉🚀 \| Accented: café résumé \| CJK: 你好世界' | All unicode characters render correctly including emojis, accented Latin chars, and CJK characters |
| 5 | Send a message containing quotes and apostrophes: 'She said "hello" and it\'s working' | Both double quotes and apostrophes display correctly without escaping artifacts (no &quot; or &EliteaAI/elitea_issues#39;) |
| 6 | Send a message with code block containing special chars: '```<html>&amp;"test"</html>```' | Code block renders with proper syntax highlighting and special characters shown literally as code |
| 7 | Reload the page and verify all previously sent messages still display correctly | Messages persist correctly after reload with no encoding corruption or character loss |
| 8 | Copy one of the special-character messages using the copy button and paste into a text editor | Copied text matches the original input without additional escaping or encoding artifacts |

## Expected Final State

Copied text matches the original input without additional escaping or encoding artifacts

## Pass/Fail Criteria

PASS: All special characters display as intended in chat, persist after reload, and copy correctly
FAIL: Any character is double-escaped (e.g., &amp;amp;), stripped, rendered as raw HTML, or corrupted after reload
