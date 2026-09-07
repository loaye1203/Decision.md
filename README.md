# Decision.md

Decision 3.0 is a pre-execution configuration checkpoint for Codex. It recommends a model and reasoning level for the upcoming task, then waits for you to apply the settings and confirm execution.

## Features

- Evaluates scope clarity, difficulty, risk, verification, context, and relevant failures.
- Considers GPT-5.6 Luna, Terra, Sol, and GPT-6 Astra across five reasoning levels: twenty candidate combinations when available.
- Compares smaller models with deeper reasoning against stronger models with lighter reasoning.
- Distinguishes token counts, token rates, and total usage including retries.
- Preserves manual configuration and project approval requirements.

Read-only discussion, research, planning, and review proceed normally. The checkpoint applies before file changes, installation, publication, deployment, or other state-changing actions.

## Choosing a configuration

| Model | Typical fit |
| --- | --- |
| GPT-5.6 Luna | Clear, bounded, repeatable work with reliable checks |
| GPT-5.6 Terra | Everyday engineering, integrations, refactoring, and ordinary debugging |
| GPT-5.6 Sol | Complex analysis, open-ended design, difficult diagnosis, and synthesis |
| GPT-6 Astra | Demanding end-to-end work across systems, tools, changing constraints, and long context |

| Reasoning label | Effort | Typical need |
| --- | --- | --- |
| 轻度 | low | Clear approach with limited exploration |
| 中 | medium | Ordinary planning, decisions, and verification |
| 高 | high | Multiple hypotheses, edge cases, or substantial checking |
| 极高 | xhigh | Deeply interacting uncertainties and extensive analysis |
| 更高（消耗更多使用额度） | max | Exceptional problems where additional exploration is likely to help |

These are task-selection guidelines, not benchmark rankings. Every available model-and-effort combination remains eligible. Decision does not assume that Astra low equals Luna high, or that the newest model always wins at every effort.

The process first assesses the required reliability, chooses a model and effort candidate, and then compares plausible alternatives. Quality requirements come first; usage preferences help choose among suitable configurations.

Ultra is considered separately as a delegation mode when available and authorized. It is not one of the five ordinary reasoning levels.

## Workflow

1. Describe the task.
2. For a state-changing task, Codex reads the rule and briefly explains the deciding factor.
3. Its final line gives exactly one recommendation, for example:

   ```text
   GPT-5.6 Terra，思考等级中
   ```

4. Codex stops. You manually select the configuration and confirm execution.
5. Codex performs the approved work under the project's existing permissions.

A materially changed workload or newly discovered capability gap triggers re-evaluation. Routine continuation does not require another checkpoint.

## Install

Download [Decision.md](./Decision.md) and place it in your Codex Home directory. For the Windows setup used here:

```text
C:\Users\<YourUser>\.codex\Decision.md
```

Add the following instruction to your global `AGENTS.md` in the same directory, substituting your actual absolute path:

```text
Before beginning any implementation or other state-changing task, you MUST read `C:\Users\<YourUser>\.codex\Decision.md`, complete the decision process it defines, output the recommended execution configuration, and wait for the user to confirm before execution. If the file cannot be read, stop and report the exact path attempted.
```

If your Codex Home location differs, use that location for both files and the instruction. Preserve any existing instructions in `AGENTS.md`. Start a new task after changing global instructions.

To update, review your local customizations and replace `Decision.md` with the desired version. Downloading or updating this repository alone does not install the rule globally.

## Limits

The rule recommends settings; it does not switch models, grant permissions, enable Ultra, or guarantee correctness or savings. Only configurations available in your client are eligible.

Model-and-effort examples are guidelines rather than measured equivalences. Actual token use and total cost depend on the task, context, checks, tools, and retries.

## Versions

- [Current Decision 3.0](./Decision.md): four models, twenty combinations, cross-model comparison, and usage-aware selection.
- [Decision 2.0](https://github.com/loaye1203/Decision.md/tree/v2.0): the previous three-model rule and README.
- [Decision 1.0](https://github.com/loaye1203/Decision.md/tree/v1.0): the original confirmation workflow.
