---
id: ELITEA-3788
title: "Verify Export Handles Missing/Deleted Attachments Gracefully"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, error-handling, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3788: Verify Export Handles Missing/Deleted Attachments Gracefully

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that the export process handles conversations with missing or deleted attachments gracefully without failing completely.

**Coverage:**
- Export continues despite missing attachments
- Available attachments are included in export
- Missing attachments noted appropriately
- JSON metadata includes reference to missing attachment
- Appropriate notification shown
- Conversation remains accessible after export

## Preconditions

- Logged in to {{base_url}}
- Conversation exists with attachments
- At least one attachment has been deleted from storage (but reference remains in conversation messages)
- User is the conversation creator

## Test Data

- Conversation with 3 attachments:
  - attachment1.png (exists)
  - attachment2.pdf (deleted/missing from storage)
  - attachment3.docx (exists)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify conversation references 3 attachments | Conversation UI shows 3 attachment references in messages |
| 2 | Verify one attachment is missing/deleted | attachment2.pdf not accessible or shows error when clicked |
| 3 | Right-click conversation | Context menu with "Export" |
| 4 | Click "Export" | Dialog opens |
| 5 | Verify dialog shows "(3 files · X MB)" or adjusted | Dialog may show original count or adjusted for missing file |
| 6 | Select "With attachments" | Radio button selected |
| 7 | Click "Export" | Export process begins |
| 8 | Verify export handles missing attachment gracefully | Export completes without crashing |
| 9 | Verify export behavior | ZIP downloads with available attachments OR error notification with partial export |
| 10 | If ZIP downloads, extract archive | Extraction succeeds |
| 11 | Navigate to attachments folder in ZIP | Attachments folder visible |
| 12 | Verify available attachments present | attachment1.png present, attachment3.docx present |
| 13 | Verify missing attachment not in ZIP | attachment2.pdf absent (expected) |
| 14 | Open JSON from ZIP | JSON structure visible |
| 15 | Verify JSON contains reference to attachment2 | Attachment2 metadata present in messages |
| 16 | Check if attachment2 marked as missing/unavailable | JSON may indicate status: "missing" or "unavailable" |
| 17 | Verify success notification or warning | Success with warning: "Chat exported successfully (1 attachment unavailable)" OR clear success message |
| 18 | Verify conversation remains accessible | Open conversation → accessible without corruption |

## Expected Final State

- Export completes with available attachments
- Missing attachment handled gracefully (not included in ZIP)
- JSON includes metadata showing attachment references
- Appropriate notification shown
- Conversation unchanged and accessible

## Pass/Fail Criteria

**Pass:**
- Export completes (doesn't crash or fail completely)
- Available attachments (attachment1, attachment3) included in ZIP
- Missing attachment (attachment2) not in ZIP but handled gracefully
- JSON includes attachment metadata/references for all 3 attachments
- Success notification or warning shown ("1 attachment unavailable")
- Conversation remains accessible

**Fail:**
- Export fails completely due to missing attachment
- Available attachments not included
- JSON corrupted or missing attachment metadata
- No notification or error message
- Conversation corrupted after export

## Postconditions

- Conversation accessible and unchanged
- User aware of missing attachment (via notification)
