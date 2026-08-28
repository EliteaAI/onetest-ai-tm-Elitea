---
id: ELITEA-2904
title: "Configuration Tab — Toolkit-Specific Field Values Preserved"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, configuration, data-preservation]
requirements: []
---
# ELITEA-2904: Configuration Tab — Toolkit-Specific Field Values Preserved

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that toolkit-specific indexing configuration fields display the values configured at creation inside the Configuration tab, and that edits to them are retained after a page refresh.

**Coverage:**
- Toolkit-specific configuration field displays its configured value for a DOCX-capable Index
- Toolkit-specific configuration field displays its configured value for a PDF-capable Index
- SharePoint include/skip file-extension fields display their configured values
- An edit to a SharePoint include/skip extension value is retained after a page refresh

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An existing DOCX-capable Index created with its toolkit-specific option enabled
- An existing PDF-capable Index created with its toolkit-specific option enabled
- An existing SharePoint Index created with specific include/skip file-extension values set

## Test Data

| Field | Value |
|-------|-------|
| Index (DOCX) | Existing DOCX-capable Index |
| Index (PDF) | Existing PDF-capable Index |
| Index (SharePoint) | Existing SharePoint Index with include/skip extensions set |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the DOCX-capable Index's details page and click "Configuration". | Configuration fields display. |
| 2 | Inspect the toolkit-specific configuration field for this toolkit type. | Field shows the value configured at creation. |
| 3 | Open the PDF-capable Index's details page and click "Configuration". | Configuration fields display. |
| 4 | Inspect the toolkit-specific configuration field for this toolkit type. | Field shows the value configured at creation. |
| 5 | Open the SharePoint Index's details page and click "Configuration". | Configuration fields display. |
| 6 | Inspect the include and skip file-extension fields. | Both fields show the values configured at creation. |
| 7 | Modify the include file-extension value and apply the update via the UI. | Value is accepted. |
| 8 | Refresh the page and click "Configuration" again. | The updated include file-extension value is still displayed. |

## Expected Final State

Each toolkit-specific field shows its correct configured value, and the edited SharePoint field retains its new value after a refresh.

## Pass/Fail Criteria

**Pass:**
- All toolkit-specific fields display the values configured at creation
- The edited value persists after a refresh

**Fail:**
- Any toolkit-specific field is missing, blank, or shows an incorrect value
- The edited value reverts or is lost after a refresh
