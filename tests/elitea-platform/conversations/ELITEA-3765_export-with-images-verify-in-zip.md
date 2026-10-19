---
id: ELITEA-3765
title: "Export Conversation With Images - Verify Images in ZIP"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3765: Export Conversation With Images - Verify Images in ZIP

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that conversations with image attachments export correctly with images preserved in the ZIP archive.

**Coverage:**
- Image files are included in ZIP export
- Images maintain original filename and format
- Images can be opened and displayed correctly
- Image file sizes match original

## Preconditions

- Logged in to {{base_url}}
- Conversation with at least 2 image attachments (.png, .jpg, .gif, etc.)
- User is the conversation creator

## Test Data

- Conversation with 2-3 image files (different formats: PNG, JPG, GIF)
- Known image filenames: e.g., "screenshot.png", "photo.jpg"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats section | Chat list displays |
| 2 | Identify conversation with image attachments | Conversation with images visible |
| 3 | Right-click conversation | Context menu with "Export" appears |
| 4 | Click "Export" | Dialog opens |
| 5 | Verify "With attachments" shows image count | e.g., "(2 files · 1.5 MB)" displayed |
| 6 | Select "With attachments" | Radio button selected |
| 7 | Click "Export" | Progress indicator appears, then ZIP downloads |
| 8 | Extract ZIP archive | Extraction succeeds |
| 9 | Navigate to attachments folder in ZIP | Attachments folder visible |
| 10 | Verify all image files present | screenshot.png and photo.jpg found |
| 11 | Verify original filenames preserved | Filenames match: "screenshot.png", "photo.jpg" |
| 12 | Verify original formats preserved | Extensions intact: .png, .jpg |
| 13 | Open screenshot.png | Image opens and displays correctly |
| 14 | Open photo.jpg | Image opens and displays correctly |
| 15 | Verify image file sizes match original | File sizes approximately match (no significant loss) |
| 16 | Open JSON from ZIP | JSON contains image attachment metadata/references |

## Expected Final State

- ZIP archive contains all image files in attachments folder
- Images have original filenames and formats
- Images can be opened and viewed
- JSON includes image metadata

## Pass/Fail Criteria

**Pass:**
- All images present in ZIP/attachments folder
- Original filenames and formats preserved (.png, .jpg, .gif)
- Images open and display correctly without corruption
- File sizes match originals
- JSON includes image references

**Fail:**
- Images missing from ZIP
- Filenames changed or formats altered
- Images corrupted or cannot be opened
- File sizes significantly different
- No image metadata in JSON

## Postconditions

- Original conversation with images unchanged
- Images remain accessible in conversation
