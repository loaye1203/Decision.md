# Decision.md

Decision 3.1 is a small pre-execution checkpoint for Codex. It recommends one model and one reasoning level for the upcoming work, then waits for the user to confirm before any state-changing action. It does not switch models or grant permissions automatically.

## Default routing

| Task class | Default model and effort | Examples |
| --- | --- | --- |
| Thinking, planning, and solution design | GPT-6 Astra, high or above | Requirements, research synthesis, architecture, technical plans, trade-offs, risk analysis, decomposition, and test strategy. |
| Execution | GPT-5.6 Luna, xhigh (极高) | Code writing/editing, implementation, refactoring, tests, debugging, scripts, document edits, image generation/editing, and tool-driven production. |

Astra uses `high` by default for thinking, `xhigh` for substantial ambiguity or risk, and `max` only for exceptional difficulty. Luna uses `xhigh` by default for execution; `max` is reserved for bounded work where extra exploration is justified.

When a request contains both phases, split it when possible: Astra for the plan, then Luna for execution. Do not treat reasoning levels across models as equivalent. GPT-5.6 Sol and GPT-5.6 Terra are exception paths only when explicitly requested, the default model is unavailable, or compatibility/reliability evidence requires them.

## What it evaluates

- Scope clarity and acceptance criteria
- Judgment, ambiguity, and task difficulty
- Consequences of mistakes and reversibility
- Dependencies, context, and verification strength
- Quality, time, and usage priorities
- Availability of the selected model and effort in the current client

All four models and five effort levels remain eligible when available. The levels are `low` (轻度), `medium` (中), `high` (高), `xhigh` (极高), and `max` (更高). They are relative to the selected model, not a universal intelligence score or token budget.

## Workflow

1. Describe the task.
2. Before the first state-changing action, Codex reads `Decision.md`, classifies the dominant phase, and assesses the relevant risks and checks.
3. Codex returns a short reason and a final line in this exact form:

   ```text
   <recommended model>，思考等级<recommended reasoning level>
   ```

4. Codex stops. You manually select the configuration and confirm execution.
5. Codex performs the approved work under the project's existing permissions.

Read-only discussion, research, review, and planning do not require the confirmation gate unless a model recommendation is requested. Re-evaluate when the task, risk, verification, availability, or relevant failure evidence materially changes.

`Ultra` is a separate delegation mode, not a sixth reasoning level. It is never enabled automatically.

## Install on Windows

Download [Decision.md](./Decision.md) and place it at:

```text
C:\Users\<YourUser>\.codex\Decision.md
```

Add this instruction to the global `AGENTS.md` in the same Codex directory, preserving any existing instructions:

```text
Before beginning any implementation or other state-changing task, you MUST read `C:\Users\<YourUser>\.codex\Decision.md`, complete the decision process it defines, output the recommended execution configuration, and wait for the user to confirm before execution. If the file cannot be read, stop and report the exact path attempted.
```

Start a new task after changing global instructions. Updating this repository does not install the rule globally; installation is a separate, deliberate copy operation.

## Versions

- [Decision 3.1 (current)](./Decision.md): Astra-first thinking, Luna-first execution, explicit exceptions, and manual confirmation.
- [Decision 3.0](https://github.com/loaye1203/Decision.md/tree/v3.0): Previous four-model configuration guidance.
- [Decision 2.0](https://github.com/loaye1203/Decision.md/tree/v2.0): Previous three-model rule and README.
- [Decision 1.0](https://github.com/loaye1203/Decision.md/tree/v1.0): Original confirmation workflow.

## Limits

The rule recommends settings; it does not switch models, create agents, enable Ultra, grant permissions, or guarantee correctness or savings. Actual usage depends on the task, context, reasoning, tools, checks, and retries.
