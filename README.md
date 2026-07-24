# Decision.md

`Decision.md` is a global Codex pre-execution rule. Before Codex performs an implementation or any other state-changing action, it recommends the model and reasoning level that should be used, then waits for the user to confirm.

## Install globally

1. Put `Decision.md` in your Codex Home directory.

   On Windows, the default location is:

   ```text
   C:\Users\<YourUser>\.codex\Decision.md
   ```

2. Create or edit the global `AGENTS.md` in the same directory:

   ```text
   C:\Users\<YourUser>\.codex\AGENTS.md
   ```

3. Add this rule to the global `AGENTS.md`, replacing `<YourUser>` with your Windows user name:

   ```text
   Before beginning any implementation or other state-changing task, you MUST read `C:\Users\<YourUser>\.codex\Decision.md`, complete the decision process it defines, output the recommended execution configuration, and wait for the user to confirm before execution. If the file cannot be read, stop and report the exact path attempted.
   ```

4. Start a new Codex task. Global `AGENTS.md` guidance is loaded when a task starts.

## How it works

1. You describe a task.
2. If it requires implementation or another state-changing action, Codex reads `Decision.md` and evaluates only the execution workload.
3. Codex finishes its normal reply first. Project-specific prompts, such as a request for approval, remain in that reply.
4. The final line is the configuration recommendation, in plain text and without a code block:

   ```text
   GPT-5.6 Terra，思考等级中
   ```

5. Codex stops. You manually switch the model and reasoning level if needed, then authorize execution according to the current project's rules.
6. If the task changes materially before execution, Codex runs the decision again.

## Notes

- The recommendation is not an automatic model switch.
- `Decision.md` does not replace a project's own approval or write-permission rules.
- Read-only questions, discussion, review, and analysis do not trigger the process unless they are followed by a request to make changes.
