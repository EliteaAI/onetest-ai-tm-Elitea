---
id: ELITEA-1157
title: "ADO Wiki — delete_page_by_path executes with page_name + wiki_identifier (wiki identifier not set in toolkit)"
priority: critical
type: functional
module: ado-wiki-toolkit
status: ready
execution_type: manual
tags: [foundbyautomation, feat:toolkits, issue:3985, ai_created, int:ado, eng:sdk, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3985]
---
# ELITEA-1157: ADO Wiki — delete_page_by_path executes with page_name + wiki_identifier (wiki identifier not set in toolkit)

**Module:** Ado Wiki Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `delete_page_by_path` successfully deletes a wiki page when the wiki identifier is not pre-configured in the toolkit (requiring both `page_name` and `wiki_identified` as explicit inputs), and that it also works with `page_name` alone when the wiki identifier is pre-configured in the toolkit.

**Coverage:**
- `delete_page_by_path` accepts `page_name` + `wiki_identified` when no default wiki identifier is set in toolkit config
- `process_images` / `image_description_prompt` parameter is no longer present in the delete_page_by_path schema
- Tool executes without `unexpected keyword argument 'process_images'` TypeError
- Wiki page is successfully deleted from ADO Wiki
- With wiki identifier pre-configured in toolkit, `delete_page_by_path` executes with `page_name` alone

## Preconditions

- Logged in to {{base_url}}
- ADO Wiki toolkit configured with valid ADO credential (e.g. `Ado_cred_sam`)
- Target wiki (`Samvel_Simonyan.wiki`) contains a page at path `/test_parent_page/test_nested_child`
- Scenario A: "Default Wiki Identifier" field is left **empty** in toolkit configuration
- Scenario B: "Default Wiki Identifier" is set to `Samvel_Simonyan.wiki`
- Fix from issue EliteaAI/elitea_issues#3985 is deployed (branch: `auto_approve_fix` or later)

## Test Data

- ELITEA URL: {{base_url}}
- Toolkit name: Ado Wiki
- `wiki_identified` (Scenario A): `Samvel_Simonyan.wiki`
- `page_name` (Scenario A): `/test_parent_page/test_nested_child`
- `page_name` (Scenario B): any valid existing page path in `Samvel_Simonyan.wiki`
- Raw JSON (Scenario A): `{"page_name": "/test_parent_page/test_nested_child", "wiki_identified": "Samvel_Simonyan.wiki"}`
- Raw JSON (Scenario B): `{"page_name": "/test_parent_page/test_nested_child"}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits. Open the ADO Wiki toolkit configuration. Clear the 'Default Wiki Identifier' field and save. | Toolkit saves successfully with the 'Default Wiki Identifier' field empty. |
| 2 | In the ADO Wiki toolkit page, open the Test Settings panel. Select tool 'Delete page by path' from the tool dropdown. | Test Settings shows input fields: 'Wiki Identified' (optional) and 'Page Name' (required). The 'process_images' or 'image_description_prompt' field is NOT visible. |
| 3 | Switch to Raw JSON input mode. Enter: {"page_name": "/test_parent_page/test_nested_child", "wiki_identified": "Samvel_Simonyan.wiki"}. Click RUN TOOL. | Tool runs successfully. Response confirms the wiki page at path '/test_parent_page/test_nested_child' was deleted. No 'unexpected keyword argument process_images' error or TypeError appears. |
| 4 | Navigate back to the ADO Wiki toolkit configuration. Set 'Default Wiki Identifier' to 'Samvel_Simonyan.wiki'. Save. | Toolkit saves with 'Default Wiki Identifier' set to 'Samvel_Simonyan.wiki'. |
| 5 | In the ADO Wiki toolkit Test Settings panel, select tool 'Delete page by path'. Enter Raw JSON: {"page_name": "/test_parent_page/test_nested_child"} (no wiki_identified field). Click RUN TOOL. | Tool executes successfully using the toolkit's pre-configured default wiki identifier. Wiki page is deleted. No parameter error appears. |

## Expected Final State

Tool executes successfully using the toolkit's pre-configured default wiki identifier. Wiki page is deleted. No parameter error appears.

## Pass/Fail Criteria

**Pass:**
- `delete_page_by_path` succeeds with `page_name` + `wiki_identified` when no default wiki identifier is configured in the toolkit
- `delete_page_by_path` succeeds with `page_name` alone when the default wiki identifier is pre-configured in the toolkit
- No `unexpected keyword argument 'process_images'` or TypeError appears in any scenario
- `process_images` / `image_description_prompt` field is absent from the delete tool schema in Test Settings

**Fail:**
- Tool returns `unexpected keyword argument 'process_images'` or similar TypeError in any run
- Tool fails when `wiki_identified` is supplied explicitly and no toolkit default is set
- Tool fails when only `page_name` is supplied and the default wiki identifier is configured
- `process_images` field is still visible in the Test Settings panel for this tool
