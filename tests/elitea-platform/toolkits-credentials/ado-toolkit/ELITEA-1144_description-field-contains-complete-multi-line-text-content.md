---
id: ELITEA-1144
title: "Description field contains complete multi-line text content"
priority: high
type: functional
module: ado-toolkit
status: ready
execution_type: manual
tags: [int:ado-repos, feat:toolkits, eng:backend, issue:4497, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4497]
---
# ELITEA-1144: Description field contains complete multi-line text content

**Module:** Ado Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that multi-line PR descriptions are returned in full without truncation or data loss, and line breaks are preserved.

**Coverage:**
- Multi-line descriptions are returned completely
- Line breaks and formatting are preserved correctly
- No truncation at arbitrary character limits
- Full content integrity maintained

## Preconditions

- User authenticated with valid ADO credentials
- ADO Toolkit configured and connected to target ADO repository
- Test ADO repository accessible with PR containing multi-line description (10+ lines)
- Environment: {{base_url}}

## Test Data

- ADO Repository: [Test repo with PRs]
- PR ID: [PR with multi-line description - e.g., PR #789]
- Expected line count: 10+ lines
- Expected description structure: Multiple paragraphs with line breaks
- Tool name: get_pull_request

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create or identify a PR in ADO with a multi-line description (10+ lines with paragraphs) | PR identified |
| 2 | Note the exact description content including line breaks | Content documented |
| 3 | Navigate to Toolkits from sidebar in ELITEA | Toolkits page loads |
| 4 | Open configured ADO Toolkit in Test Settings | Test Settings opens |
| 5 | Select get_pull_request tool | Tool selected |
| 6 | Enter PR ID with multi-line description | PR ID entered |
| 7 | Execute the tool | Tool executes |
| 8 | Review the description field in the response | Description visible |
| 9 | Verify all lines are present (count matches expected) | All lines present |
| 10 | Verify line breaks are preserved between paragraphs | Line breaks preserved |
| 11 | Compare retrieved description with original PR description in ADO | Content matches |

## Expected Final State

Content matches

## Pass/Fail Criteria

**Pass:**
- Description field contains all lines from PR description
- Line breaks are preserved correctly
- No truncation occurs
- Content matches original PR description exactly
- Full text integrity maintained

**Fail:**
- Description is truncated or incomplete
- Line breaks are lost or corrupted
- Content does not match original PR description
- Only first N lines are returned
- Text formatting is corrupted
