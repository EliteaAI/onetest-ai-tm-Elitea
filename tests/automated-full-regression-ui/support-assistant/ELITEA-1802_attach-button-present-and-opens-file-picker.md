---
id: ELITEA-1802
title: "Attach button is present and opens file picker in Support Assistant"
priority: medium
type: functional
module: support-assistant
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-1802: Attach button is present and opens file picker in Support Assistant

**Module:** support-assistant · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Attach file button is visible in the Support Assistant input area, that clicking it triggers the browser's native file-chooser dialog, and that a file can be selected through that dialog.

---

## Preconditions

- User is authenticated (browser context pre-loaded with `auth_state` via `page` fixture).
- A temporary test file (`test_attachment.txt` with content `"Test attachment content"`) is created by the `tmp_path` pytest fixture.
- Support Assistant feature is enabled.

---

## Test Data

| Field | Value |
|-------|-------|
| Attach button selector | `button[aria-label="Attach file"]` |
| Test file name | `test_attachment.txt` |
| Test file content | `"Test attachment content"` |
| Network idle timeout | 10 000 ms |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chat page (`/chat`) | Page loads successfully |
| 2 | Open the Support Assistant widget | Widget panel opens; title is visible |
| 3 | Wait for the widget to be fully ready | Widget title and message input are visible |
| 4 | Assert that the Attach file button is visible | `page.locator('button[aria-label="Attach file"]').first.is_visible()` returns `True` |
| 5 | Click the Attach file button while listening for a file-chooser event | `page.expect_file_chooser(timeout=10000)` context manager is active; `attach_btn.click()` is executed; browser opens a native file-chooser dialog |
| 6 | Assert that a file-chooser dialog was opened | `FileChooser` object (`fc_info.value`) is not `None` |
| 7 | Select the temporary test file (`test_attachment.txt`) in the file chooser | `file_chooser.set_files(str(test_file))` sets `tmp_path/test_attachment.txt` as the chosen file |
| 8 | Wait for network activity to settle after upload (up to 10 s) | `networkidle` state is reached |

---

## Expected Final State

The Attach file button is visible in the Support Assistant input toolbar. Clicking it opens the browser's native file-chooser dialog. After selecting the test file, network activity settles, indicating the file upload request has been processed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Attach button is visible in the widget input area.
- File-chooser dialog opens on button click.
- Network settles after file selection.

**Fail:**
- Any step produces an error or unexpected result.
- Attach button is not visible.
- File-chooser dialog does not open within the timeout.

---

## Postconditions

The temporary file (`tmp_path/test_attachment.txt`) is automatically removed by pytest's `tmp_path` fixture at the end of the test.
