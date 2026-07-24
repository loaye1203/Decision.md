# Decision.md

Version: 1.0

## Purpose

Before beginning an execution task, Codex MUST evaluate the work it is about to perform and recommend an execution configuration to the user.

Decision is a confirmation step. It does not switch the model or reasoning level automatically.

The user applies the recommended configuration manually and then confirms whether execution may begin.

## When Decision Applies

Decision applies when a user request will lead to implementation or another state-changing action.

Decision does not apply to discussion, explanation, analysis, review, or other read-only work unless the user subsequently asks Codex to execute changes.

## Input

Decision may use:

- The current User Request
- Relevant context from the current conversation
- Any plan or requirements already confirmed by the user
- The minimum read-only project context needed to understand the execution workload
- The execution configurations currently available to the user

Decision evaluates only the work that Codex is about to execute.

Decision MUST NOT:

- Change or expand the User Request
- Redesign an already confirmed solution
- Perform implementation
- Modify files or external state
- Claim that it changed the model or reasoning level

## Evaluation

Before recommending a configuration, evaluate:

- Scope: how much work must be executed
- Complexity: how difficult the implementation is
- Risk: the possible impact of mistakes or production changes
- Context size: how much project context must remain available
- Execution reasoning: how much reasoning is required while performing the work

Use the evaluation only to select the execution configuration. Do not turn Decision into a second planning phase.

## Configuration Selection

Recommend one model from the options currently available to the user.

Expected model options:

- GPT-5.6 Sol
- GPT-5.6 Terra
- GPT-5.6 Luna

Recommend one reasoning level:

- 轻度
- 中
- 高
- 极高
- 更高（消耗更多使用额度）

Select the configuration in this priority order:

1. Correctness
2. Reliability
3. Execution quality

Do not optimize for token usage, cost, or response speed unless the User Request explicitly requires it.

Never recommend a model or reasoning level known to be unavailable. If availability cannot be confirmed, state that clearly instead of inventing a configuration.

## Output

Before execution, complete any normal response required by the current task or project rules, including clarification, explanation, or a project-specific authorization request.

The final line of the response MUST be the recommendation, written as plain text on one line:

`<recommended model>，思考等级<recommended reasoning level>`

Do not add a heading, code block, label, reason, explanation, or any content after this line.

After outputting the recommendation, stop and wait for the user.

Do not begin implementation in the same response.

## User Confirmation

The user manually applies the recommended configuration and confirms that execution may begin.

The exact confirmation wording is determined by the current project's own rules. Decision does not define or replace project-specific write permissions or approval requirements.

Codex MUST NOT claim that the configuration was changed unless the user confirms it.

## Re-evaluation

The recommendation remains valid while the requested execution work remains materially unchanged.

Run Decision again before execution if:

- The user changes the requirements
- The implementation scope changes materially
- New information substantially changes the complexity, risk, context size, or reasoning requirement

Otherwise, continue with the previously recommended configuration after the user confirms execution.

## Principle

The user decides what work is required.

Decision recommends how Codex should be configured to execute that work.

The user applies the configuration and authorizes execution.

Codex then executes the confirmed task.
