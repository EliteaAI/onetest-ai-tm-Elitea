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
