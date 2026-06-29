---
id: ELITEA-1773
title: "SharePoint Personal URL — Read .xlsx File from Sharing Link"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, file-operations, xlsx, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054]
---
# ELITEA-1773: SharePoint Personal URL — Read .xlsx File from Sharing Link

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the SharePoint toolkit successfully retrieves and extracts data from .xlsx Excel files stored in personal SharePoint using sharing links.

## Preconditions

- Personal SharePoint credential configured and connected
- .xlsx file (< 5MB) uploaded to personal SharePoint
- Sharing link generated for the .xlsx file
- Agent configured with SharePoint toolkit

## Test Data

- Test file: `data-table.xlsx` with sheets, headers, data rows
- Sharing link format: `https://epam-my.sharepoint.com/:x:/p/username/...`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat with SharePoint-enabled agent | Chat interface opens |
| 2 | Send message: "Read data from this Excel file: [personal-sharepoint-xlsx-sharing-link]" | Agent processes request |
| 3 | Agent invokes "Read file from sharing link" tool | Tool execution starts |
| 4 | Wait for spreadsheet processing | Tool completes within 15 seconds |
| 5 | Observe extracted data in response | Excel data displayed (cells, rows, columns) |
| 6 | Verify sheet structure captured | Sheet names identified; Tabular data or structured content visible |

## Expected Final State

Excel data successfully extracted and displayed in structured format

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully
- Spreadsheet data extracted
- Sheet names and data structure preserved
- Tabular format recognizable in response

**Fail:**
- Tool returns error
- Empty response or no data extracted
- Data corruption or encoding issues
