# Decision.md

Version: 2.0

## Purpose

Before beginning implementation or another state-changing task, Codex MUST recommend an execution configuration to the user.

Decision does not switch the model or reasoning level. The user applies the recommendation manually and confirms before execution begins.

Choose the configuration that is sufficient for the specific task. Do not default to the strongest model or highest reasoning level.

## When Decision Applies

Decision applies before any task that creates, edits, moves, deletes, installs, publishes, deploys, sends, or otherwise changes files or external state.

Decision does not apply to discussion, explanation, analysis, research, review, planning, or other read-only work.

For a mixed request, Decision MUST finish before the first state-changing action.

## Boundaries

Decision evaluates only the work about to be executed.

Decision MUST NOT:

- Change or expand the user's request
- Redesign an already confirmed solution
- Perform implementation
- Modify files or external state
- Claim that it changed the model or reasoning level
- Recommend an unavailable configuration

## Evaluation

Evaluate only the factors needed to select a configuration:

- **Clarity:** Are the result, scope, and acceptance criteria clear?
- **Difficulty:** Is the work mechanical, ordinary, or deeply analytical?
- **Risk:** How serious and reversible would a mistake be?
- **Verification:** Can tests, builds, checks, or exact comparisons confirm the result?
- **Context:** How much code and prior state must remain coherent during execution?
- **Failure history:** Has a lower configuration already failed for a reasoning-related cause?

Task size alone does not determine the model. Strong verification may make a smaller model suitable for a large mechanical task. Weak verification or high risk may require a stronger model for a small change.

## Model Selection

Choose one model currently available to the user.

### GPT-5.6 Luna

Use Luna for clear, bounded, low-risk, and easily verified work that requires little architectural judgment.

Typical tasks:

- Mechanical or repetitive edits
- Small fixes with a known cause
- Implementation from a complete plan
- Focused tests, documentation, metadata, or configuration changes
- Bounded refactors protected by strong tests

### GPT-5.6 Terra

Use Terra for normal engineering work that requires meaningful reasoning but has manageable ambiguity and risk.

Typical tasks:

- Everyday feature implementation
- Multi-file changes following established patterns
- Ordinary debugging with a limited hypothesis space
- Moderate refactors, integrations, or dependency updates
- Work with partial verification and some implementation judgment

### GPT-5.6 Sol

Use Sol when execution depends on the strongest available judgment, sustained coherence, or careful handling of consequential uncertainty.

Typical tasks:

- Ambiguous architecture or competing designs
- Difficult diagnosis across multiple subsystems
- Security, authorization, payments, privacy, concurrency, or data integrity
- Complex migrations, recovery, or hard-to-reverse production changes
- Large unfamiliar systems with important implicit constraints
- High-risk work with weak verification
- A lower model failed because it could not maintain or resolve the required reasoning

Do not choose Sol merely because the task changes code, contains many files, or is important.

## Reasoning-Level Selection

Choose one reasoning level independently from the model.

### 轻度

Use for direct, localized, low-risk work with explicit instructions and strong verification.

### 中

Use as the normal level for ordinary implementation, moderate multi-file changes, and bounded debugging with a known approach.

### 高

Use when cross-file reasoning, root-cause analysis, non-obvious edge cases, compatibility concerns, or careful verification materially affect the result.

### 极高

Use for difficult work with several interacting uncertainties, such as architecture, subtle state transitions, concurrency, security, complex migrations, or sparse verification.

### 更高（消耗更多使用额度）

Use only when the task is exceptionally difficult and extended exploration or verification is likely to change the outcome. Do not select it solely because the task is large, important, or uses Sol.

## Selection Rules

Apply these rules in order:

1. Determine the reliability required by the task's risk and reversibility.
2. Select the model according to ambiguity, judgment, and sustained-context needs.
3. Select reasoning according to the depth of analysis and verification needed.
4. If two configurations are both sufficient, recommend the lower one.
5. Use cost, speed, or quota as deciding factors only when the user prioritizes them or when capability is otherwise equivalent.
6. Escalate the model for a capability gap; escalate reasoning for a depth-of-analysis gap.

Common starting points:

| Task type | Recommendation |
| --- | --- |
| Mechanical and strongly verified | GPT-5.6 Luna，思考等级轻度 |
| Bounded implementation from a complete plan | GPT-5.6 Luna，思考等级中 |
| Normal everyday implementation | GPT-5.6 Terra，思考等级中 |
| Non-trivial debugging or refactoring | GPT-5.6 Terra，思考等级高 |
| Difficult or high-risk work | GPT-5.6 Sol，思考等级高 |
| Ambiguous architecture or several serious uncertainties | GPT-5.6 Sol，思考等级极高 |
| Exceptional quality-first work requiring extended exploration | GPT-5.6 Sol，思考等级更高（消耗更多使用额度） |

The table gives starting points. The evaluation factors control the final choice.

## Output

Before execution, give only the brief explanation required by the current task or project rules. State the main reason for the configuration without producing another plan.

The final line MUST be:

`<recommended model>，思考等级<recommended reasoning level>`

Do not add a heading, label, code block, explanation, or any content after that line.

After outputting the recommendation, stop and wait for the user. Do not begin execution in the same response.

## Confirmation and Re-evaluation

The user manually applies the recommendation and confirms whether execution may begin. Codex MUST NOT claim that the configuration changed unless the user confirms it.

The recommendation remains valid while the execution work remains materially unchanged.

Run Decision again only if:

- The user materially changes the requirements
- New information materially changes the difficulty, risk, verification, or context needs
- A failed attempt exposes a capability or reasoning gap
- The available configurations change
