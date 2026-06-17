---
id: ELITEA-1147
title: "Description field handles special characters and markdown correctly"
priority: high
type: functional
module: ado-toolkit
status: ready
execution_type: manual
tags: [int:ado-repos, feat:toolkits, eng:backend, issue:4497, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4497]
---
# ELITEA-1147: Description field handles special characters and markdown correctly

**Module:** Ado Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that PR descriptions containing special characters, markdown formatting, and unicode/emoji are returned correctly without escaping or corruption.

**Coverage:**
- Special characters (!@#$%^&*) are returned unescaped
- Markdown formatting (links, code blocks, lists, bold, italic) is preserved
- Unicode and emoji characters are handled correctly
- No character encoding issues

## Preconditions

- User authenticated with valid ADO credentials
- ADO Toolkit configured and connected to target ADO repository
- Test ADO repository accessible with PR containing description with special chars/markdown
- Environment: {{base_url}}

## Test Data

- ADO Repository: [Test repo with PRs]
- PR ID: [PR with special chars/markdown - e.g., PR #101]
- Expected content examples:
  - Special chars: !@#$%^&*()_+-={}[]|:";'<>?,./
  - Markdown: **bold**, *italic*, `code`, [link](url), - list item
  - Unicode/emoji: 🚀 ✅ ❌ 你好
- Tool name: get_pull_request

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create or identify a PR in ADO with description containing special characters, markdown, and emoji | PR identified |
| 2 | Document the exact description content | Content documented |
| 3 | Navigate to Toolkits from sidebar in ELITEA | Toolkits page loads |
| 4 | Open configured ADO Toolkit in Test Settings | Test Settings opens |
| 5 | Select get_pull_request tool | Tool selected |
| 6 | Enter PR ID with special content | PR ID entered |
| 7 | Execute the tool | Tool executes |
| 8 | Review the description field in the response | Description visible |
| 9 | Verify special characters (!@#$%^&*) appear unescaped | Characters unescaped |
| 10 | Verify markdown syntax is preserved (**, *, `, [](url), etc.) | Markdown preserved |
| 11 | Verify unicode/emoji characters render correctly | Unicode/emoji intact |
| 12 | Compare retrieved content with original PR description character-by-character | Content matches |

## Expected Final State

Content matches

## Pass/Fail Criteria

**Pass:**
- Special characters are returned exactly as-is (unescaped)
- Markdown syntax is preserved correctly
- Unicode and emoji characters are intact
- No character encoding errors
- Content matches original PR description exactly

**Fail:**
- Special characters are escaped or corrupted (e.g., &amp; instead of &)
- Markdown syntax is stripped or altered
- Unicode/emoji characters are corrupted or replaced with �
- Character encoding issues appear
- Content does not match original
