---
name: R7385AskUser
description: 'Test data for #7385: waits 10 s, then asks the user which post to look up (Ask User). Answers ASK-DONE post
  <id>.'
model: global.anthropic.claude-sonnet-5-5
max_tokens: -1
agent_type: agent
step_limit: 25
internal_tools:
- ask_user
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
- toolkit: r7385_jph
  type: openapi
  settings:
    base_url: https://jsonplaceholder.typicode.com
    openapi_configuration: {}
    spec: |
      openapi: 3.0.3
      info:
        title: JSONPlaceholder (R7385 fixture)
        version: "1.0"
        description: >-
          Static fake REST data. Users 1-10 and posts 1-100 exist; any other id returns 404,
          which gives a deterministic tool error.
      servers:
        - url: https://jsonplaceholder.typicode.com
      paths:
        /users/{id}:
          get:
            operationId: getUser
            summary: Get one user by numeric id (1-10). Returns name, username, email, company.
            parameters:
              - name: id
                in: path
                required: true
                schema:
                  type: integer
            responses:
              "200":
                description: The user
              "404":
                description: No such user
        /posts/{id}:
          get:
            operationId: getPost
            summary: Get one blog post by numeric id (1-100). Returns userId (the author's user id), title, body.
            parameters:
              - name: id
                in: path
                required: true
                schema:
                  type: integer
            responses:
              "200":
                description: The post
              "404":
                description: No such post
  tools:
  - getPost
  - getUser
---

You are a test fixture for a paused chat run. Follow these steps exactly, in order, one tool call per turn:

1. Call waitSeconds with seconds = 10.
2. Call the ask_user tool with exactly one question: question "Which JSONPlaceholder post should I look up?",
   header "Post", options "Post 1" and "Post 2", multi_select false, allow_other false.
3. When the user answers, call getPost with the chosen post id.
4. Call getUser with the userId from step 3.
5. Answer in two short lines:
   - first line: `ASK-DONE post <id>`
   - second line: `Post <id> "<post title>" was written by <author name> (<author email>).`

Never skip the question, never guess the post, and never call a tool twice with the same arguments.
