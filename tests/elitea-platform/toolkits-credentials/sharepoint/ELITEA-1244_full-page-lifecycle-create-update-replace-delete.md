---
id: ELITEA-1244
title: "Full page lifecycle: create, update, replace, delete"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2355, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2355]
---
# ELITEA-1244: Full page lifecycle: create, update, replace, delete

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify the full OneNote page lifecycle — creating a notebook, section, and page; updating via patch_commands; replacing full content; and deleting — all complete correctly.

**Coverage:**
- onenote_create_notebook / onenote_create_section / onenote_create_page (with valid HTML including title tag)
- onenote_update_page with patch_commands append action
- onenote_replace_page_content with plain HTML fragment
- onenote_delete_page and verification via onenote_get_pages

## Preconditions

- SharePoint toolkit with Delegated OAuth auth
- At least one existing notebook available as parent

## Test Data

- New notebook name: TC4-TestNotebook
- New section name: TC4-Section
- Create page HTML: <!DOCTYPE html><html><head><title>TC4-Page</title></head><body><h1>Hello from TC4</h1><p>Initial content.</p></body></html>
- Patch command (append): [{"target": "body", "action": "append", "content": "<p>Appended by TC4.</p>"}]
- Replace content (plain fragment, no html/head wrapper): <h1>Replaced</h1><p>Updated TC4 content.</p>

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `Onenote create notebook` with display_name="TC4-TestNotebook". | Notebook created; id, displayName, createdDateTime, webUrl returned. |
| 2 | Invoke `Onenote create section` with the returned notebook_id and display_name="TC4-Section". | Section created; id, displayName, pagesUrl returned. |
| 3 | Invoke `Onenote create page` with the returned section_id and HTML including <title>TC4-Page</title>. | Page created; id, title, createdDateTime, webUrl returned. |
| 4 | Invoke `Onenote read page` to verify creation. | Content matches the initial HTML provided (heading and paragraph present). |
| 5 | Invoke `Onenote update page` with patch_commands: [{"target": "body", "action": "append", "content": "<p>Appended by TC4.</p>"}]. | Update succeeds; success confirmation string returned. |
| 6 | Invoke `Onenote read page` to verify the update. | Appended paragraph is present in the page content alongside original content. |
| 7 | Invoke `Onenote replace page content` with plain HTML fragment <h1>Replaced</h1><p>Updated TC4 content.</p> (no <html>/<head> wrapper). | Replace succeeds; success confirmation string returned. |
| 8 | Invoke `Onenote read page` again. | Only the replaced content is present — original and appended content are gone. |
| 9 | Invoke `Onenote delete page` for the created page. | Deletion succeeds; success confirmation string returned. |
| 10 | Invoke `Onenote get pages` for the section. | Deleted page no longer appears in the pages list. |

## Expected Final State

Deleted page no longer appears in the pages list.

## Pass/Fail Criteria

**Pass:**
- Full lifecycle completes without error; content correct at each stage; deleted page not retrievable

**Fail:**
- Any step errors; patch/replace content not reflected; deleted page still listed
