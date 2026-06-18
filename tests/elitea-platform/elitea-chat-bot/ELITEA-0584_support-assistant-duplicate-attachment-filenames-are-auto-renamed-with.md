---
id: ELITEA-0584
title: "Support Assistant — Duplicate Attachment Filenames Are Auto-Renamed With Timestamp Suffix"
priority: high
type: functional
module: elitea-chat-bot
status: deprecated
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0584: Support Assistant — Duplicate Attachment Filenames Are Auto-Renamed With Timestamp Suffix

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that attaching two files with the same filename does not produce an error; the second file is automatically renamed with a timestamp/size suffix and both files appear as separate attachments.

**Coverage:**
- Second file with same name as existing attachment is accepted without error
- Second file is auto-renamed with a distinguishing suffix (timestamp + size)
- Both files appear as separate thumbnails in compose area
- Both files are sent and the bot processes both

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)
- Two different image files both saved as image.png (different content, same filename)

## Test Data

- image.png (copy 1 — first file, different content from copy 2)
- image.png (copy 2 — second file, same filename, different content)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget | Empty composer |
| 2 | Attach the first image.png via click-to-browse | Thumbnail for "image.png" appears in compose area. Counter shows "9 left". |
| 3 | Attach the second image.png (same filename, different content) via click-to-browse | No error is shown. Second file is attached. Its displayed name is auto-renamed (e.g., "image_20260522_143022_1.50KB.png") — distinct from the first. |
| 4 | Verify both thumbnails are visible with distinct names/identifiers | Two separate thumbnails visible with different names/identifiers |
| 5 | Type "Please compare the two images." and click Send | Message with both files (original + renamed) sent. Bot responds acknowledging two images. |
| 6 | Observe conversation history to confirm both files are stored | Both files visible in the sent message with their respective names |

## Expected Final State

Both files visible in the sent message with their respective names

## Pass/Fail Criteria

**Pass:**
- Second file with same name is accepted without error
- Second file is auto-renamed with a distinguishing suffix
- Both files appear as separate, distinct attachments
- Both files are sent and referenced in the response

**Fail:**
- Error "File already exists" shown when attaching duplicate filename
- Only one of the two files is attached (first or second overwrites the other)
- Both show the same name (indistinguishable duplicates)
- Either file is missing from the sent message
