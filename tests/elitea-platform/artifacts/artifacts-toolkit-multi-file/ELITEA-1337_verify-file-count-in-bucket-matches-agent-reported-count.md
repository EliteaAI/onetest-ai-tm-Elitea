---
id: ELITEA-1337
title: "Verify file count in artifact bucket exactly matches number of files agent reported creating"
priority: high
type: regression
module: artifacts
status: draft
execution_type: manual
tags: [r-2.0.4, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#5313]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An agent with Artifact toolkit attached exists
- The target bucket is empty before the test (or file count is noted before running)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Agent prompt | "Create and save exactly 5 files: output-1.txt, output-2.txt, output-3.txt, output-4.txt, output-5.txt — each with unique content. List the filenames you saved in your response." |
| Expected file count | 5 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/artifacts`, open the configured bucket, and note the current file count | Baseline file count is recorded |
| 2 | Navigate to the agent and send the 5-file creation prompt | Agent responds and lists all 5 filenames in its reply |
| 3 | Record the 5 filenames from the agent response | Filenames: output-1.txt, output-2.txt, output-3.txt, output-4.txt, output-5.txt |
| 4 | Navigate back to `{{base_url}}/app/artifacts` and open the bucket | File list is displayed |
| 5 | Count the total new files added (current count minus baseline) | Exactly 5 new files appear |
| 6 | Verify each expected filename is present in the list | All 5 filenames from the agent response are found |
| 7 | Download all 5 files and verify each has unique correct content | Each file has distinct content |

## Expected Final State

The artifact bucket contains exactly 5 new files matching the names reported by the agent. No files are silently lost, overwritten, or duplicated.

## Pass/Fail Criteria

**Pass:**
- Exactly 5 new files appear in the bucket
- All 5 filenames match those reported by the agent
- Each file downloads with distinct correct content

**Fail:**
- Fewer than 5 new files appear (file loss)
- Any file reported by the agent is absent from the bucket
- Any two files share identical content when they should be distinct
