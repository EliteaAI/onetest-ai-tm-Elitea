---
id: ELITEA-3868
title: "MDX Syntax Highlighting in Raw Mode"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-3868: MDX Syntax Highlighting in Raw Mode

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify Raw mode has proper MDX/Markdown syntax highlighting

## Preconditions

- MDX file is open in Canvas

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open MDX file in Canvas | File opens |
| 2 | Switch to Raw mode | Raw mode activates |
| 3 | Observe Markdown heading syntax (#, ##, ###) | Headings highlighted |
| 4 | Observe text formatting (**bold**, *italic*, `code`) | Formatting highlighted |
| 5 | Observe import/export statements (if present) | Statements highlighted |
| 6 | Observe JSX tags (if present) | Tags highlighted |
| 7 | Observe code blocks (```jsx) | Blocks highlighted |
| 8 | Observe comments | Comments highlighted |

## Expected Results

- Markdown syntax is highlighted (headings, bold, italic, etc.)
- JSX/MDX-specific syntax is highlighted (imports, exports, components)
- Code blocks are distinguished with different background or styling
- Comments are colored distinctly
- Syntax highlighting improves code readability
- Different syntax elements use distinct colors

## Pass/Fail Criteria

**Pass:**
- All MDX/Markdown syntax properly highlighted
- Colors are distinct and readable
- Code readability is improved

**Fail:**
- No syntax highlighting
- Incorrect highlighting
- Colors are confusing or hard to read
