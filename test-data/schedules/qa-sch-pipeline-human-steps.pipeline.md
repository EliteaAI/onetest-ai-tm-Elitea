---
name: QA-SCH Pipeline human steps
description: 'QA test data for schedules (#7011): versions with a step that waits for a person, so schedules are Blocked.
  v base = HITL node, v printer = Printer node. Do not change.'
model: global.openai.gpt-5.6-luna
max_tokens: -1
agent_type: pipeline
step_limit: 25
entry_point: Review
nodes:
- id: Review
  type: hitl
  input:
  - messages
  user_message:
    type: fixed
    value: Approve to continue.
  routes:
    approve: LLM 1
    reject: END
- id: LLM 1
  type: llm
  input: []
  input_mapping:
    chat_history:
      type: fixed
      value: []
    system:
      type: fixed
      value: Answer with the word OK.
    task:
      type: fixed
      value: Say OK
  output: []
  structured_output: false
  transition: END
pipeline_settings:
  edges:
  - id: xy-edge__Reviewapprove---LLM 1
    data: {}
    type: custom
    source: Review
    target: LLM 1
    sourceHandle: hitlNode_approve
  - id: xy-edge__Reviewreject---END
    data: {}
    type: custom
    source: Review
    target: END
    sourceHandle: hitlNode_reject
  - id: xy-edge__LLM 1---EliteAPipelineEnd
    type: custom
    source: LLM 1
    target: END
  nodes:
  - id: END
    data:
      label: End
    type: END
    measured:
      width: 100
      height: 44
    position:
      x: 170
      y: 538
  - id: Review
    data:
      label: Review
    type: hitl
    measured:
      width: 320
      height: 139
    position:
      x: 60
      y: 60
  - id: LLM 1
    data:
      label: LLM 1
    type: llm
    measured:
      width: 320
      height: 119
    position:
      x: -158
      y: 287
  orientation: vertical
  layout_version: '1.0'
---

