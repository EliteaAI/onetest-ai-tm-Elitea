---
id: ELITEA-4456
title: "Create Project Backup modal opens with the exact specified text and default selection; both chat-inclusive radio options are disabled with the correct tooltip when the project has zero chats"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4456: Create Backup modal: exact default state, and both chat-inclusive options disabled on a chat-free project

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A brand-new project ("Project A") with zero chats of any kind (no chats, no run-history-derived
  conversations) at the time of this test.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | In Project A, go to Settings → General. Locate the **Back Up & Restore** section. Read its description text. | Reads exactly: **"Back up this project's data to be able to restore it, if needed. Your backup will be downloaded as an encrypted file and will include agents, pipelines, toolkits, MCP servers and skills, and optionally all chats with or without their attachments. Credentials, tokens and other secrets will be excluded from this backup file and cannot be restored."** Two buttons are present: **"Create a Backup"** and **"Restore from the Backup"**. |
| 2 | Click **"Create a Backup"**. | A modal opens titled **"Create Project Backup"**. **No file downloads immediately.** |
| 3 | Read the modal's description text. | Reads exactly: **"Back up the data of \<Project A's name\>. Agents, pipelines, toolkits, MCP servers and skills are always included. Credentials, tokens and other secrets are excluded."** |
| 4 | Look at the **Chats** radio group and its default selection. | Three options shown: **"Do not include chats"**, **"All chats without attachments"**, **"All chats with attachments"**. **"Do not include chats" is selected by default.** |
| 5 | Try to select **"All chats without attachments"**, then **"All chats with attachments"**. | Both options are **disabled** (not selectable) — Project A has zero chats. Hovering either shows the tooltip **"This project has no chats"**. "Do not include chats" remains enabled and selected. |
| 6 | Confirm the buttons present. | **Cancel** and **Backup** buttons are both present and enabled. |

### Expected Final State
The Settings page section text, the modal's default text, default selection, and zero-chats disabled state all match the specification exactly.

### Pass/Fail Criteria
**Pass:** All quoted text matches exactly; both chat-inclusive options are disabled with the correct tooltip.
**Fail:** Any wording mismatch, wrong default selection, or either chat-inclusive option remaining selectable on a chat-free project.
