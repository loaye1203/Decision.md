# Decision.md

`Decision.md` is a small global rule for Codex that adds a manual configuration checkpoint before execution.

When a task will change files or external state, Codex evaluates the work, recommends one model and one reasoning level, and stops. You apply the recommendation manually and confirm before Codex begins execution.

The rule is designed to choose a configuration that is sufficient for the task instead of always defaulting to the strongest model or highest reasoning level.

## What it does

- Runs before implementation and other state-changing actions
- Does not run for discussion, explanation, research, planning, review, or other read-only work
- Evaluates task clarity, difficulty, risk, verification, context, and earlier failures
- Selects the model and reasoning level separately
- Gives one concise recommendation in a fixed format
- Waits for the user to switch the configuration and approve execution
- Re-evaluates only when the task or its risk changes materially

## What it does not do

- It does not switch the model automatically.
- It does not perform implementation during the recommendation step.
- It does not expand or redesign the user's request.
- It does not replace project permissions, safety rules, or destructive-action confirmations.
- It does not assume that a larger task always needs a stronger model.

## How configuration is selected

Decision considers six factors:

| Factor | Question |
| --- | --- |
| Clarity | Are the scope, result, and acceptance criteria clear? |
| Difficulty | Is the work mechanical, ordinary, or deeply analytical? |
| Risk | How serious and reversible would a mistake be? |
| Verification | Can tests, builds, checks, or exact comparisons confirm the result? |
| Context | How much code and prior state must remain coherent? |
| Failure history | Has a lower configuration already failed for a reasoning-related cause? |

Task size is not enough by itself. A large mechanical change with strong tests may use a smaller model, while a small security-sensitive change with weak verification may need a stronger one.

### Model guide

| Model | Best fit |
| --- | --- |
| GPT-5.6 Luna | Clear, bounded, low-risk, strongly verified work; mechanical edits; implementation from a complete plan |
| GPT-5.6 Terra | Everyday engineering, ordinary multi-file changes, moderate debugging, and manageable ambiguity |
| GPT-5.6 Sol | Difficult diagnosis, ambiguous architecture, high-risk systems, weak verification, or sustained cross-system reasoning |

### Reasoning guide

| Level | Best fit |
| --- | --- |
| 轻度 | Direct, localized, low-risk work with strong verification |
| 中 | Normal implementation and bounded debugging with a known approach |
| 高 | Cross-file reasoning, root-cause analysis, edge cases, compatibility, or careful verification |
| 极高 | Several interacting uncertainties, such as architecture, concurrency, security, or complex migrations |
| 更高（消耗更多使用额度） | Exceptional quality-first work where extended exploration can materially change the outcome |

Higher reasoning is not automatically better. Decision uses the lowest configuration that is still expected to meet the task's reliability needs.

## Workflow

1. You ask Codex to perform a task.
2. If the task is read-only, Codex proceeds normally.
3. If the task changes state, Codex reads `Decision.md` and evaluates only the upcoming execution.
4. Codex briefly explains the deciding factor.
5. The final line contains the recommendation:

   ```text
   GPT-5.6 Terra，思考等级中
   ```

6. Codex stops without implementing anything.
7. You manually apply the recommended model and reasoning level, then confirm execution.
8. Codex performs the task under the normal project permissions and safety rules.

If the requirements, risk, or available configurations change materially before execution, Codex runs the decision step again.

## Install globally

1. Download [`Decision.md`](./Decision.md).

2. Put it in your Codex Home directory. On Windows, the default location is:

   ```text
   C:\Users\<YourUser>\.codex\Decision.md
   ```

3. Create or edit the global `AGENTS.md` in the same directory:

   ```text
   C:\Users\<YourUser>\.codex\AGENTS.md
   ```

4. Add the following instruction, replacing `<YourUser>` with your Windows user name:

   ```text
   Before beginning any implementation or other state-changing task, you MUST read `C:\Users\<YourUser>\.codex\Decision.md`, complete the decision process it defines, output the recommended execution configuration, and wait for the user to confirm before execution. If the file cannot be read, stop and report the exact path attempted.
   ```

5. Start a new Codex task so the global `AGENTS.md` guidance is loaded.

## Updating

Replace the global `Decision.md` with the newer repository version, then start a new Codex task. Existing tasks may continue using instructions that were loaded when they started.

Review local customizations before replacing the file. The repository update does not change your Codex configuration automatically.

## Versions

- [`main`](https://github.com/loaye1203/Decision.md/blob/main/Decision.md) contains the current Decision 2.0 rule.
- [`v1.0`](https://github.com/loaye1203/Decision.md/tree/v1.0) preserves the original Decision 1.0 rule and README.
