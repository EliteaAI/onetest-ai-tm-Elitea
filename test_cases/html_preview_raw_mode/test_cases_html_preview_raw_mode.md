# Test Cases: HTML Preview and Raw Mode

**Feature**: [Enhancement] Add HTML Source and Preview Modes for Artifacts and Chat Results  
**Issue**: #5845  
**Sub-issues**: #5767 (Closed), #5926 (Open - Dark theme text visibility bug)

---

## Test Cases

### **P0 - Critical Test Cases**

#### **TC-HTML-P0-001: Open HTML file from Artifacts in Preview mode**
**Priority**: P0  
**Objective**: Verify HTML files open correctly from Artifacts bucket in Preview mode by default  
**Preconditions**:
- User is logged into Elitea
- Artifacts bucket contains HTML files (e.g., html-htm/script folder)
- User has access to the Artifacts section

**Test Steps**:
1. Navigate to Artifacts section
2. Select bucket: "Elitea S3 storage"
3. Navigate to folder: html-htm > script
4. Click on an HTML file (e.g., `test_file_2_between_1_3mb_structured.htm`)
5. Observe the Canvas/File Preview opens

**Expected Results**:
- File opens in Canvas mode
- "Preview" tab is selected by default
- "Html (detected)" is displayed in the file type indicator
- HTML content renders correctly showing formatted content (headings, text, images, tables, etc.)
- "Raw" tab is visible and clickable
- File path breadcrumb shows: html-htm > script > [filename]

**Test Data**: 
- File: `test_file_2_between_1_3mb_structured.htm`
- Expected content: "Comprehensive Test Report 2 - Between 1MB and 3MB" with Executive Dashboard

---

#### **TC-HTML-P0-002: Switch from Preview to Raw mode**
**Priority**: P0  
**Objective**: Verify user can switch from Preview mode to Raw mode to view HTML source code  
**Preconditions**:
- HTML file is open in Canvas in Preview mode

**Test Steps**:
1. With HTML file open in Preview mode
2. Click on "Raw" tab
3. Observe the display changes to Raw mode

**Expected Results**:
- Canvas switches to Raw mode
- HTML source code is displayed
- Code has syntax highlighting (HTML tags colored)
- Line numbers are visible
- Code is properly formatted and readable
- Same file name and path remain in header

**Test Data**: 
- Use `test_file_2_between_1_3mb_structured.htm` from Artifacts

---

#### **TC-HTML-P0-003: Edit HTML in Raw mode and save changes**
**Priority**: P0  
**Objective**: Verify user can edit HTML source in Raw mode and save changes  
**Preconditions**:
- HTML file is open in Raw mode
- User has write permission

**Test Steps**:
1. Open HTML file in Raw mode
2. Locate the `<title>` tag (around line 6)
3. Change the title text from existing title to "TEST EDIT - Modified Title"
4. Observe Save button state
5. Click "Save" button
6. Switch to Preview mode

**Expected Results**:
- Code editor allows text editing
- Save button becomes active (changes from gray to purple) after modification
- Clicking Save successfully saves the changes
- No error messages appear
- Switching to Preview mode shows updated title in the rendered HTML

**Test Data**: 
- Original title: "Comprehensive Test Report 2 - Between 1MB and 3MB"
- Modified title: "TEST EDIT - Modified Title"

---

#### **TC-HTML-P0-004: Discard unsaved changes**
**Priority**: P0  
**Objective**: Verify Discard functionality restores the last saved version  
**Preconditions**:
- HTML file is open in Raw mode
- Changes have been made but not saved

**Test Steps**:
1. Open HTML file in Raw mode
2. Make changes to HTML source (e.g., change a heading text)
3. Observe Save and Discard buttons are active
4. Click "Discard" button
5. Observe warning dialog appears
6. Click "Confirm" button in the warning dialog

**Expected Results**:
- Discard button is active when changes are made
- Warning dialog displays with:
  - Title: "Warning"
  - Message: "You are editing now. Do you want to discard current changes and continue?"
  - Buttons: "Cancel" and "Confirm" (red button)
- Clicking "Cancel" keeps the editor open with changes intact
- Clicking "Confirm" restores the original content and discards changes
- Save button becomes inactive after confirming discard

---

#### **TC-HTML-P0-005: Preview mode renders HTML content correctly**
**Priority**: P0  
**Objective**: Verify HTML content renders properly in Preview mode with all formatting  
**Preconditions**:
- HTML file with rich content is available in Artifacts

**Test Steps**:
1. Open `test_file_2_between_1_3mb_structured.htm` in Preview mode
2. Scroll through the entire document
3. Verify all content types render correctly:
   - Headings (h1, h2, h3)
   - Text formatting (bold, italic, underlined, strikethrough, highlighted)
   - Dashboard cards with statistics
   - Tables
   - Lists
   - Inline CSS styles
   - Background colors and gradients

**Expected Results**:
- All HTML elements render correctly
- CSS styles are applied
- Dashboard shows 4 colored cards (Total Revenue, Total Users, Performance, Engagement)
- Text formatting showcase displays: bold red text, italic green text, underlined text, strikethrough text, highlighted yellow background
- Tables render with proper borders and structure
- Colors, fonts, and spacing match the HTML/CSS definitions
- No broken layouts or missing content

---

#### **TC-HTML-P0-006: Open HTML file generated in chat with View/Edit button**
**Priority**: P0  
**Objective**: Verify HTML files generated in chat can be opened in Canvas from chat interface  
**Preconditions**:
- User is in a chat session
- Agent has Artifacts toolkit available

**Test Steps**:
1. Send prompt to agent: "create an assistant landing page file in html format with headings, text formatting, lists, tables, images, inline styles, CSS styles within the HTML file, and report/dashboard layouts"
2. Wait for agent to generate HTML file
3. Observe the chat response with generated file artifact
4. Locate "View/Edit file" button/tooltip on the file artifact
5. Click "View/Edit file"

**Expected Results**:
- Agent generates HTML file successfully
- File appears in chat as a clickable artifact item with file name (e.g., "assistant-landing-page.html")
- File artifact shows file icon and name
- Hovering or interacting shows "View/Edit file" action
- Clicking "View/Edit file" opens the file in Canvas
- Canvas opens in Preview mode by default
- HTML renders correctly in Preview mode
- Can switch to Raw mode if needed

**Test Data**: 
- Generated file: `assistant-landing-page.html` or similar

---

#### **TC-HTML-P0-007: Close Canvas with unsaved changes shows warning**
**Priority**: P0  
**Objective**: Verify closing Canvas with unsaved changes triggers warning dialog  
**Preconditions**:
- HTML file is open in Raw mode
- Changes have been made but not saved

**Test Steps**:
1. Open HTML file in Raw mode
2. Make changes to HTML source (e.g., add a comment)
3. Click the "X" (Close) button in Canvas header
4. Observe warning dialog appears

**Expected Results**:
- Warning dialog displays before closing with:
  - Title: "Warning"
  - Message: "You are editing now. Do you want to discard current changes and continue?"
  - Buttons: "Cancel" and "Confirm" (red button)
- Clicking "Cancel" keeps Canvas open with changes intact
- Clicking "Confirm" closes Canvas and discards changes

---

### **P1 - High Priority Test Cases**

#### **TC-HTML-P1-001: Unsaved changes preserved when switching modes**
**Priority**: P1  
**Objective**: Verify unsaved changes are preserved when switching between Preview and Raw modes  
**Preconditions**:
- HTML file is open in Raw mode

**Test Steps**:
1. Open HTML file in Raw mode
2. Make a change (e.g., modify a heading text)
3. Do NOT save
4. Click to switch to Preview mode
5. Observe warning dialog appears (if applicable)
6. Confirm switching if prompted
7. Switch back to Raw mode

**Expected Results**:
- Warning dialog may appear: "You are editing now. Do you want to discard current changes and continue?"
- If warning appears, clicking "Confirm" switches to Preview mode
- Preview shows the modified content (if unsaved changes are preserved) or original content (if changes discarded)
- Mode switching behavior is consistent

---

#### **TC-HTML-P1-002: Preview refreshes after saving changes in Raw mode**
**Priority**: P1  
**Objective**: Verify Preview mode updates to show saved changes  
**Preconditions**:
- HTML file is open in Raw mode

**Test Steps**:
1. Open HTML file in Raw mode
2. Change a visible element (e.g., change "Executive Dashboard" to "TEST Dashboard")
3. Save changes
4. Switch to Preview mode

**Expected Results**:
- Preview mode displays the updated content
- Change is visible in rendered HTML (shows "TEST Dashboard" instead of "Executive Dashboard")
- No stale cache or old content is displayed

---

#### **TC-HTML-P1-003: Copy Content from three-dot menu**
**Priority**: P1  
**Objective**: Verify Copy Content option copies HTML source to clipboard  
**Preconditions**:
- HTML file is open in Canvas

**Test Steps**:
1. Open HTML file in Canvas (any mode)
2. Click three-dot menu (⋮) in top-right corner
3. Click "Copy Content" option
4. Open a text editor (e.g., Notepad)
5. Paste (Ctrl+V)

**Expected Results**:
- Three-dot menu shows "Copy Content", "Download", and "Delete" options
- Clicking "Copy Content" copies HTML source code to clipboard
- Pasted content shows full HTML source code
- Content is identical to Raw mode view

---

#### **TC-HTML-P1-004: Download HTML file from three-dot menu**
**Priority**: P1  
**Objective**: Verify Download option downloads HTML file to local machine  
**Preconditions**:
- HTML file is open in Canvas

**Test Steps**:
1. Open HTML file in Canvas
2. Click three-dot menu (⋮)
3. Click "Download" option
4. Check browser downloads

**Expected Results**:
- File downloads to local machine
- Downloaded file has correct name with .html or .htm extension
- Downloaded file contains correct HTML source code
- File can be opened in local browser and renders correctly

---

#### **TC-HTML-P1-005: HTML without color styles is readable in Dark theme**
**Priority**: P1 (Linked to bug #5926)  
**Objective**: Verify HTML files without explicit color styles are readable in Dark theme  
**Preconditions**:
- Elitea UI is set to Dark theme
- HTML file without color definitions is available

**Test Steps**:
1. Set Elitea UI to Dark theme (Settings > Theme > Dark)
2. Navigate to Artifacts > html-htm
3. Open `test_file_1_under_1mb.htm` (file without explicit color styles)
4. Observe text visibility in Preview mode

**Expected Results**:
- Text is clearly visible and readable
- Text color is light/white (not black on dark background)
- Background adapts to dark theme or remains readable
- No black-on-black or invisible text issues
- Content is fully readable without straining

**Note**: This test validates the fix for bug #5926

---

#### **TC-HTML-P1-006: Switch to Raw mode shows syntax highlighting**
**Priority**: P1  
**Objective**: Verify Raw mode has proper HTML syntax highlighting  
**Preconditions**:
- HTML file is open

**Test Steps**:
1. Open HTML file in Canvas
2. Switch to Raw mode
3. Observe code syntax highlighting

**Expected Results**:
- HTML tags (e.g., `<html>`, `<body>`, `<div>`) are colored distinctly
- Attribute names are highlighted
- Attribute values are colored differently
- Strings are colored
- Comments are colored distinctly (if present)
- Syntax highlighting improves code readability

---

#### **TC-HTML-P1-007: File type shows "Html (detected)"**
**Priority**: P1  
**Objective**: Verify file type is correctly detected and displayed  
**Preconditions**:
- HTML file is open in Canvas

**Test Steps**:
1. Open any .html or .htm file from Artifacts
2. Observe the file type indicator in Canvas header

**Expected Results**:
- File type shows "Html (detected)" 
- Type indicator is visible next to file name
- Indicator appears in both Preview and Raw modes

---

### **P2 - Medium Priority Test Cases**

#### **TC-HTML-P2-001: Open .htm file (alternate extension)**
**Priority**: P2  
**Objective**: Verify .htm extension files are treated same as .html  
**Preconditions**:
- Artifacts bucket contains .htm files

**Test Steps**:
1. Navigate to Artifacts > html-htm > script
2. Locate a .htm file (e.g., `test_file_3_greater_5mb.htm`)
3. Click to open

**Expected Results**:
- .htm file opens in Canvas same as .html
- File type shows "Html (detected)"
- Preview and Raw modes work identically to .html files
- No errors or warnings about file extension

---

#### **TC-HTML-P2-002: Delete HTML file from three-dot menu**
**Priority**: P2  
**Objective**: Verify Delete option removes file from Artifacts  
**Preconditions**:
- Test HTML file exists in Artifacts (create a copy for testing)
- User has delete permission

**Test Steps**:
1. Open HTML file in Canvas
2. Click three-dot menu (⋮)
3. Click "Delete" option
4. Observe confirmation dialog
5. Confirm deletion
6. Navigate to Artifacts folder where file was located

**Expected Results**:
- Delete option triggers confirmation dialog
- Confirmation dialog asks "Are you sure you want to delete this file?"
- Confirming deletion removes file from Artifacts
- Canvas closes after deletion
- File no longer appears in Artifacts bucket/folder

**Note**: Use a test copy file for this test to avoid losing important files

---

#### **TC-HTML-P2-003: HTML with images renders images correctly**
**Priority**: P2  
**Objective**: Verify images within HTML are displayed in Preview mode  
**Preconditions**:
- HTML file contains image tags (either embedded or external URLs)

**Test Steps**:
1. Create or locate HTML file with `<img>` tags
2. Open in Preview mode
3. Observe image rendering

**Expected Results**:
- Images with valid URLs display correctly
- Image positioning and sizing match HTML/CSS definitions
- Broken image URLs show broken image icon or placeholder
- No errors in browser console for valid images

---

#### **TC-HTML-P2-004: HTML with external CSS references**
**Priority**: P2  
**Objective**: Verify HTML with external CSS links handles gracefully  
**Preconditions**:
- HTML file contains `<link rel="stylesheet" href="...">` to external CSS

**Test Steps**:
1. Create or locate HTML with external CSS link
2. Open in Preview mode
3. Observe styling

**Expected Results**:
- External CSS loads if accessible
- If CSS is blocked (security), HTML renders without styling or with default styles
- No error messages to user
- HTML structure is still readable

---

#### **TC-HTML-P2-005: Empty HTML file opens without error**
**Priority**: P2  
**Objective**: Verify empty HTML files can be opened  
**Preconditions**:
- Empty HTML file exists in Artifacts (0 bytes or only whitespace)

**Test Steps**:
1. Navigate to empty HTML file in Artifacts
2. Click to open

**Expected Results**:
- File opens in Canvas
- Preview mode shows blank/empty content
- Raw mode shows empty editor or whitespace
- No error messages
- Can switch between modes
- Can edit and add content in Raw mode

---

#### **TC-HTML-P2-006: Malformed HTML renders with best effort**
**Priority**: P2  
**Objective**: Verify malformed HTML doesn't crash Canvas and shows content  
**Preconditions**:
- HTML file with syntax errors (e.g., unclosed tags, missing DOCTYPE)

**Test Steps**:
1. Create or locate HTML with malformed syntax
2. Open in Preview mode
3. Switch to Raw mode

**Expected Results**:
- Preview mode renders HTML with best-effort (browser auto-correction)
- Some content may be visible despite errors
- No Canvas crash or browser freeze
- Raw mode shows the source as-is with errors
- User can edit and fix errors in Raw mode

---

#### **TC-HTML-P2-007: Multiple HTML files can be opened simultaneously**
**Priority**: P2  
**Objective**: Verify multiple HTML files can be opened in separate Canvas instances  
**Preconditions**:
- Multiple HTML files exist in Artifacts

**Test Steps**:
1. Open first HTML file in Canvas
2. Navigate back to Artifacts (without closing first Canvas)
3. Open second HTML file
4. Observe both Canvas instances

**Expected Results**:
- Second file opens in a new Canvas tab/window
- Both files are accessible
- Switching between files works correctly
- Each file maintains its own state (Preview/Raw mode, edits)
- No interference between files

---

#### **TC-HTML-P2-008: Script tags do not execute in Preview mode (Security)**
**Priority**: P2  
**Objective**: Verify JavaScript in HTML does not execute for security  
**Preconditions**:
- HTML file contains `<script>` tags with JavaScript code

**Test Steps**:
1. Create or locate HTML with `<script>alert("XSS Test")</script>`
2. Open in Preview mode
3. Observe browser behavior

**Expected Results**:
- No JavaScript alert appears
- Scripts are blocked/disabled in Preview iframe
- No security warnings
- Page renders HTML/CSS only
- Console shows no script execution errors

**Security Note**: This validates the sandbox requirement from the issue

---

#### **TC-HTML-P2-009: HTML with special characters renders correctly**
**Priority**: P2  
**Objective**: Verify HTML with special characters (UTF-8, symbols, etc.) displays properly  
**Preconditions**:
- HTML file contains special characters: é, ñ, ü, ™, ©, ®, emojis, etc.

**Test Steps**:
1. Create or locate HTML with special characters
2. Open in Preview mode
3. Switch to Raw mode

**Expected Results**:
- Special characters display correctly in Preview mode
- UTF-8 encoding is properly handled
- Characters don't appear as garbled text or question marks
- Raw mode shows correct character representation
- Editing preserves special characters

---

#### **TC-HTML-P2-010: File breadcrumb navigation works correctly**
**Priority**: P2  
**Objective**: Verify file path breadcrumb is displayed and functional  
**Preconditions**:
- HTML file is in nested folder structure

**Test Steps**:
1. Open HTML file from: Elitea S3 storage > html-htm > script > test_file_2_between_1_3mb_structured.htm
2. Observe breadcrumb in Canvas header
3. Verify path shows full hierarchy

**Expected Results**:
- Breadcrumb shows: html-htm > script > [filename]
- Path is clear and readable
- Breadcrumb helps user understand file location
- Optional: Breadcrumb parts are clickable to navigate back to folder

---

## Test Summary

**Total Test Cases**: 26
- **P0 (Critical)**: 7 test cases
- **P1 (High Priority)**: 7 test cases  
- **P2 (Medium Priority)**: 12 test cases

**Coverage Areas**:
- Artifacts HTML file opening (P0)
- Preview/Raw mode switching (P0, P1)
- Editing and saving (P0, P1)
- Chat-generated HTML files (P0)
- File actions (P1, P2)
- Theme compatibility (P1)
- Security and sandboxing (P2)
- Edge cases and error handling (P2)

**Known Issues to Validate**:
- #5926: Dark theme text visibility bug (TC-HTML-P1-005)

**Test Environment**: 
- DEV: https://dev.elitea.ai
- Test bucket: Elitea S3 storage > html-htm > script

**Test Data Files**:
- `test_file_1_under_1mb.htm` (18.9 KB)
- `test_file_2_between_1_3mb_structured.htm` (19.0 KB)
- `test_file_3_greater_5mb.htm` (25.4 KB - structured)
- `test_file_3_greater_5mb.htm` (30.0 KB - structured variant)
- Chat-generated: `assistant-landing-page.html` (generated on demand)
