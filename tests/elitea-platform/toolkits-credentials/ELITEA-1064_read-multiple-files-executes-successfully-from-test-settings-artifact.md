---
id: ELITEA-1064
title: "Read multiple files executes successfully from Test Settings (Artifact toolkit)"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5002]
---
# ELITEA-1064: Read multiple files executes successfully from Test Settings (Artifact toolkit)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that filling in valid file paths and clicking RUN TOOL in the Artifact toolkit Test Settings returns file contents without errors.

**Coverage:**
- File Paths* field accepts a valid JSON array
- RUN TOOL button becomes enabled after required field is filled
- Tool executes and returns file contents in the chat panel
- No crash or error overlay during execution

## Preconditions

- Logged into {{base_url}}
- Artifact toolkit (e.g. "Artifact regression", bucket: regr) is configured with "Read multiple files" enabled
- At least one file exists in the bucket (e.g. test.txt)

## Test Data

- Toolkit: "Artifact regression", bucket: regr
- File Paths input: ["test.txt"]
- Bucket Name: leave empty (uses toolkit default)
- Offset: leave empty
- Limit: leave empty

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits and open the Artifact regression toolkit. | Toolkit detail page is shown with Test Settings panel on the right. |
| 2 | In the Test Settings panel, open the Tool dropdown and select 'Read multiple files'. | Form renders with File Paths*, Bucket Name, Offset, Limit, and Skip Size Check fields. RUN TOOL button is visible but disabled. |
| 3 | In the File Paths* field, enter ["test.txt"]. | Input is accepted. RUN TOOL button becomes enabled. |
| 4 | Leave Bucket Name, Offset, and Limit fields empty. | Fields remain empty. |
| 5 | Click RUN TOOL. | Loading indicator appears in the chat panel. |
| 6 | Wait for the response in the chat panel. | Response contains the content of test.txt from the regr bucket. No error overlay or JS crash occurs. |

## Expected Final State

Response contains the content of test.txt from the regr bucket. No error overlay or JS crash occurs.

## Pass/Fail Criteria

**Pass:**
- RUN TOOL executes without crashing the page
- Chat panel displays file contents or a meaningful API response

**Fail:**
- Page crashes with any error overlay after clicking RUN TOOL
- Response contains an unexpected server error unrelated to input validation
