---
id: ELITEA-1658
title: "SO10 - fstring Templates"
priority: high
type: functional
module: structured-output
status: ready
execution_type: automated
tags: [structured_output, templates, llm_node, fstring]
requirements: []
---
# ELITEA-1658: SO10 - fstring Templates

**Module:** Structured Output · **Priority:** High · **Type:** Functional

**Objective:** Verify fstring task templates work correctly with complex variable interpolation in LLM nodes, producing correct structured output with the interpolated values.

## Preconditions

Pipeline engine is running and accessible
LLM model (gpt-4o or equivalent) is configured and accessible
No external toolkit or service credentials required
Test pipeline YAML: suites/structured_output/tests/test_case_10_fstring_templates.yaml

## Test Data

output_format: "JSON"
num_items: 3
category: "technology"
include_metadata: true
Entry point: generate_with_fstring
Node 1 (generate_with_fstring): type=llm, fstring system prompt uses {output_format} and {category}, fstring task uses {num_items}, {category}, {output_format}, {include_metadata}
Node 2 (verify_output): type=code, validates fstring vars and output structure

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize pipeline state with fstring config variables: output_format='JSON', num_items=3, category='technology', include_metadata=true | State variables are set correctly before pipeline execution |
| 2 | Execute pipeline starting at node 'generate_with_fstring' (LLM node) with fstring system prompt: 'You are a data generator that produces output in {output_format} format. You specialize in generating content for the {category} category.' | LLM node resolves {output_format}='JSON' and {category}='technology' in the system prompt via fstring interpolation |
| 3 | LLM node executes with fstring task template interpolating {num_items}=3, {category}='technology', {output_format}='JSON', {include_metadata}=true | LLM receives the fully interpolated prompt and generates structured output for generated_items, metadata, and status |
| 4 | Verify LLM structured output is parsed using structured_output_dict: generated_items='list[dict]', metadata='dict', status='str' | generated_items is a list of dicts, metadata is a dict, status is a str — all types correct |
| 5 | Pipeline transitions to 'verify_output' code node; code reads fstring config vars from alita_state and checks output_format='JSON', num_items=3, category='technology', include_metadata=True | fstring_checks dict: output_format_set=True, num_items_set=True, category_set=True, include_metadata_set=True; fstring_interpolation_working=True |
| 6 | Code node verifies output structure: generated_items is list, len(generated_items)==3, all items are dicts with 'name' key, metadata is dict, status is str | output_checks dict: generated_items_is_list=True, generated_items_count_correct=True, items_are_dicts=True, metadata_is_dict=True, status_is_str=True |
| 7 | Code node verifies metadata and status: metadata contains 'category' key, status.lower()=='success' | metadata_checks: metadata_has_category=True, status_is_success=True |
| 8 | Check final test_results.test_passed value from code node output | test_results.test_passed=True, item_structure_valid=True, actual_values.generated_items_count=3 |

## Expected Final State

test_results.test_passed=True, item_structure_valid=True, actual_values.generated_items_count=3

## Pass/Fail Criteria

PASS: test_results.test_passed is True and fstring_interpolation_working is True and generated_items contains exactly 3 dict items each with a 'name' key
FAIL: Any fstring variable is not correctly interpolated in the LLM prompt
FAIL: generated_items is not a list, is empty, or items are not dicts
FAIL: len(generated_items) != 3
FAIL: metadata is not a dict or does not contain 'category'
FAIL: status is not the string 'success'
