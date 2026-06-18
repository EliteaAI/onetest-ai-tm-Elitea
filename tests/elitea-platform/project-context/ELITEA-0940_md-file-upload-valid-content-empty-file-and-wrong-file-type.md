---
id: ELITEA-0940
title: ".md File Upload — Valid Content, Empty File, and Wrong File Type"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, file-upload, story:3395, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0940: .md File Upload — Valid Content, Empty File, and Wrong File Type

**Module:** Project Context · **Priority:** High · **Type:** Functional

**Objective:** Verify that .md file upload works correctly for valid content, handles empty files, and rejects wrong file types.

**Coverage:**
- Valid .md file uploads and replaces editor content
- Content not persisted until Save is clicked
- Empty .md file clears editor
- Non-.md file extension is rejected

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Valid .md content: `# My Project

**Stack:** Node.js, React

**Rules:**
- Respond concisely
- Cite sources`
- Empty .md: a file with 0 bytes
- Wrong type: a file named `context.txt` with any text content

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as Editor (Private project). Create a .md file with the following content: '# My Project\n\n**Stack:** Node.js, React\n\n**Rules:**\n- Respond concisely\n- Cite sources'. Upload it via the Upload button. | Content loads into the editor, replacing previous content. |
| 2 | Do NOT click Save. Reload the page. | Uploaded content is lost — not persisted until Save is explicitly clicked. |
| 3 | Upload the same file again. Click Save. | Content persists after reload. |
| 4 | Create an empty .md file (0 bytes). Upload it. Click Save. | Editor becomes empty. Reload confirms empty content. No error shown. |
| 5 | Attempt to upload a file with a .txt extension containing the same text as the valid .md file. | File is not selectable in the upload dialog (filtered out), OR an error appears: only .md files are supported. |
| 6 | Log in as Admin/Editor in a Team project. Repeat steps 1–5. | Same behavior in Team project. |

## Expected Final State

Same behavior in Team project.

## Pass/Fail Criteria

**Pass:**
- Valid .md file loads and saves correctly
- Upload without save does not persist
- Empty .md clears editor after save
- .txt file rejected

**Fail:**
- Upload auto-saves without user clicking Save
- .txt file accepted
- Empty file causes error
