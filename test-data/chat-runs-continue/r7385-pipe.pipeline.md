---
name: R7385Pipe
description: 'Test data for #7385: waitSeconds 10, LLM, waitSeconds 10, LLM (about 25 s). Answers PIPE-DONE <word>.'
model: global.anthropic.claude-sonnet-5-5
max_tokens: -1
agent_type: pipeline
step_limit: 25
toolkits:
- toolkit: r7385_echo
  type: openapi
  settings:
    base_url: https://postman-echo.com
    openapi_configuration: {}
    spec: |
      openapi: 3.0.3
      info:
        title: Postman Echo delay (R7385 fixture)
        version: "1.0"
        description: >-
          Public, no auth. GET /delay/{seconds} answers after that many seconds (0-10), which gives the
          R7385 agents a deterministic latency knob.
      servers:
        - url: https://postman-echo.com
      paths:
        /delay/{seconds}:
          get:
            operationId: waitSeconds
            summary: Wait the given number of seconds (0-10) and return {"delay":"<seconds>"}.
            parameters:
              - name: seconds
                in: path
                required: true
                schema:
                  type: integer
                  minimum: 0
                  maximum: 10
            responses:
              "200":
                description: Waited
  tools:
  - waitSeconds
state:
  input:
    type: str
  messages:
    type: list
entry_point: Wait1
nodes:
- id: Wait1
  type: toolkit
  input:
  - input
  output:
  - messages
  structured_output: false
  transition: Think1
  toolkit_name: r7385_echo
  tool: waitSeconds
  input_mapping:
    seconds:
      type: fixed
      value: 10
- id: Think1
  type: llm
  prompt:
    type: string
    value: ''
  input:
  - input
  output:
  - messages
  structured_output: false
  transition: Wait2
  input_mapping:
    system:
      type: fixed
      value: 'You are a test fixture. Reply with exactly one line: PIPE-STEP 1'
    task:
      type: fstring
      value: '{input}'
    chat_history:
      type: fixed
      value: []
- id: Wait2
  type: toolkit
  input:
  - input
  output:
  - messages
  structured_output: false
  transition: Think2
  toolkit_name: r7385_echo
  tool: waitSeconds
  input_mapping:
    seconds:
      type: fixed
      value: 10
- id: Think2
  type: llm
  prompt:
    type: string
    value: ''
  input:
  - input
  output:
  - messages
  structured_output: false
  transition: END
  input_mapping:
    system:
      type: fixed
      value: 'You are a test fixture. Reply with exactly one line: PIPE-DONE <the word the user gave, or NONE>'
    task:
      type: fstring
      value: '{input}'
    chat_history:
      type: fixed
      value: []
---
