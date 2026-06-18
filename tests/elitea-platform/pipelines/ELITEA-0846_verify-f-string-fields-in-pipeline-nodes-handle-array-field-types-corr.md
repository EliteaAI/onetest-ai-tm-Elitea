---
id: ELITEA-0846
title: "Verify f-string fields in pipeline nodes handle Array field types correctly"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines]
requirements: []
---
# ELITEA-0846: Verify f-string fields in pipeline nodes handle Array field types correctly

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** F-string type fields in pipeline nodes always return string values, even when the field type is set to Array. This causes errors when downstream nodes expect array data but receive a string. This test verifies that f-string fields correctly handle and preserve data types including Arrays.

## Preconditions

User logged into Elitea stage.elitea.ai
User can create pipelines with Code nodes and State modifier nodes
Understanding of f-string field configuration in pipeline nodes

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new pipeline with a Code node that outputs an Array value (e.g., a Python list of items like ['item1', 'item2', 'item3']) | Pipeline is created with a Code node configured to return an array/list value |
| 2 | Add a second node (LLM or Code) that receives the output from the first Code node via an f-string field configured as Array type | Second node is added and connected. The f-string field is configured with Array type to receive the upstream array output |
| 3 | In the second node, configure the f-string field to reference the first node's output (e.g., {{Code_1.output}}) | F-string field is configured with the reference to the upstream node's array output |
| 4 | Add an END node and connect the second node to it. Save the pipeline | Pipeline is saved successfully with the complete flow: Code (array output) -> Node with f-string Array field -> END |
| 5 | Execute the pipeline by sending a message in the embedded chat | Pipeline executes without errors. The f-string field correctly passes the array data (not a string representation) to the downstream node |
| 6 | Open the run details and examine the data type passed through the f-string field | The f-string field value is an actual Array type, not a string like '[item1, item2]'. The downstream node receives proper array data |
| 7 | Verify the downstream node processed the array correctly (e.g., iterated over items, checked length, or performed array operations) | Downstream node successfully performed array operations without type errors. No 'string is not iterable' or similar type mismatch errors |
| 8 | Modify the Code node to return an empty array ([]) and re-execute the pipeline | Pipeline handles empty array gracefully — downstream node receives an empty array (not null, not empty string). No errors from empty array processing |
| 9 | Modify the Code node to return a nested array (e.g., [['a', 'b'], ['c', 'd']]) and re-execute the pipeline | Nested array structure is preserved through the f-string field — downstream node receives proper nested array, not a flattened string representation |
| 10 | Modify the Code node to return a mixed-type array (e.g., [1, 'text', True, {'key': 'value'}]) and re-execute the pipeline | Mixed-type array is passed correctly — all element types (int, string, boolean, object) are preserved in the downstream node. No type coercion or data loss |
| 11 | Switch the f-string field type from Array to String, re-execute the pipeline, and verify the behavior difference | With String type, the array is converted to its string representation. This confirms the Array type setting is actually being respected and makes a difference in data handling |

## Expected Final State

With String type, the array is converted to its string representation. This confirms the Array type setting is actually being respected and makes a difference in data handling

## Pass/Fail Criteria

PASS: Array data passes through f-string fields with correct Array type preserved; downstream nodes can perform array operations; empty, nested, and mixed-type arrays handled correctly; Array vs String type setting produces different behavior
FAIL: F-string fields convert Array values to strings, causing type errors or data corruption in downstream nodes; empty or nested arrays fail; no behavioral difference between Array and String type settings
