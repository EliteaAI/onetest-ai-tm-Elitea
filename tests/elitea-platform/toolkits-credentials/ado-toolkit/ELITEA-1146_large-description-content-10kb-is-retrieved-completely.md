---
id: ELITEA-1146
title: "Large description content (>10KB) is retrieved completely"
priority: medium
type: functional
module: ado-toolkit
status: ready
execution_type: manual
tags: [int:ado-repos, feat:toolkits, eng:backend, issue:4497, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4497]
---
# ELITEA-1146: Large description content (>10KB) is retrieved completely

**Module:** Ado Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that very large PR descriptions (>10KB) are retrieved completely without truncation and tool performance remains acceptable.

**Coverage:**
- Very long PR descriptions are returned in full
- No truncation at arbitrary length limits
- Tool performance remains acceptable (< 30 seconds)
- No timeout or memory issues

## Preconditions

- User authenticated with valid ADO credentials
- ADO Toolkit configured and connected to target ADO repository
- Test ADO repository accessible with PR containing large description (>10KB text)
- Environment: {{base_url}}

## Test Data

- ADO Repository: [Test repo with PRs]
- PR ID: [PR with large description >10KB - e.g., PR EliteaAI/elitea_issues#999]
- Expected description size: >10KB (approximately 10,000+ characters)
- Tool name: get_pull_request
- Performance target: < 30 seconds execution time

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create or identify a PR in ADO with a very large description (>10KB - e.g., multiple pages of text, tables, code samples) | PR identified |
| 2 | Measure the exact character/byte count of the description | Size documented |
| 3 | Navigate to Toolkits from sidebar in ELITEA | Toolkits page loads |
| 4 | Open configured ADO Toolkit in Test Settings | Test Settings opens |
| 5 | Select get_pull_request tool | Tool selected |
| 6 | Enter PR ID with large description | PR ID entered |
| 7 | Execute the tool and start timer | Tool executes |
| 8 | Wait for execution to complete and stop timer | Execution completes |
| 9 | Review the description field in the response | Description visible |
| 10 | Verify complete description is returned (character count matches) | Full content returned |
| 11 | Verify no truncation occurred | No truncation |
| 12 | Verify execution time is acceptable (< 30 seconds) | Performance acceptable |

## Expected Final State

Performance acceptable

## Pass/Fail Criteria

**Pass:**
- Complete description is returned (full 10KB+ content)
- No truncation at any length limit
- Execution completes within 30 seconds
- No timeout errors
- No memory or performance issues

**Fail:**
- Description is truncated (partial content returned)
- Tool times out or fails
- Execution exceeds 30 seconds
- Memory errors occur
- Performance is unacceptable
