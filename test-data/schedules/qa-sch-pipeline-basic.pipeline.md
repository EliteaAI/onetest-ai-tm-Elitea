---
name: QA-SCH Pipeline basic
description: 'QA test data for schedules (#7011): LLM node then Artifact create_file node (sensitive). Use with Run mode Entry
  point or Prompt. Do not change.'
model: global.openai.gpt-5.6-luna
max_tokens: -1
agent_type: pipeline
step_limit: 25
state:
  bucket_name:
    type: str
    value: qa-sch
  content:
    type: str
    value: created by a scheduled pipeline run
  create_result:
    type: str
  delete_result:
    type: str
  filename:
    type: str
    value: qa-sch-pipeline.txt
entry_point: LLM 1
nodes:
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
  tool_names: {}
  transition: Create file
- id: Create file
  type: toolkit
  input:
  - filename
  - bucket_name
  - content
  input_mapping:
    bucket_name:
      type: variable
      value: bucket_name
    filedata:
      type: variable
      value: content
    filename:
      type: variable
      value: filename
  output:
  - create_result
  structured_output: true
  tool: create_file
  toolkit_name: qa-sch-pipeline-artifact
  transition: Delete file
- id: Delete file
  type: toolkit
  input:
  - filename
  - bucket_name
  input_mapping:
    bucket_name:
      type: variable
      value: bucket_name
    filename:
      type: variable
      enum:
      - bucket_name
      - content
      - create_result
      - delete_result
      - filename
      value: filename
  output:
  - delete_result
  structured_output: true
  tool: delete_file
  toolkit_name: qa-sch-pipeline-artifact
  transition: END
toolkits:
- toolkit: qa-sch-pipeline-artifact
  type: artifact
  settings:
    bucket: qa-sch
    embedding_model: text-embedding-3-small
    pgvector_configuration:
      private: false
      elitea_title: elitea-pgvector
      configuration_type: pgvector
  tools:
  - create_file
  - delete_file
pipeline_settings:
  edges:
  - id: xy-edge__LLM 1---Create file
    data: {}
    type: custom
    source: LLM 1
    target: Create file
  - id: xy-edge__Create file---Delete file
    data: {}
    type: custom
    source: Create file
    target: Delete file
  - id: xy-edge__Delete file---EliteAPipelineEnd
    type: custom
    source: Delete file
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
      y: 787
  - id: LLM 1
    data:
      label: LLM 1
    type: llm
    measured:
      width: 320
      height: 119
    position:
      x: 60
      y: 60
  - id: Create file
    data:
      label: Create file
    type: toolkit
    measured:
      width: 320
      height: 139
    position:
      x: -166
      y: 298
  - id: Delete file
    data:
      label: Delete file
    type: toolkit
    measured:
      width: 320
      height: 139
    position:
      x: 60
      y: 538
  orientation: vertical
  layout_version: '1.0'
---

