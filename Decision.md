# Decision.md

Version: 3.0

## Purpose and Scope

Before implementation or any state-changing action, recommend one execution configuration, then stop for user confirmation. The user manually selects the model and reasoning level.

Read-only discussion, research, review, and planning do not trigger Decision. For mixed requests, complete Decision before the first state-changing action.

Evaluate only the upcoming execution. Do not expand the request, redesign a confirmed solution, implement changes, or claim to switch settings during Decision. Project permissions and safety requirements still apply.

## Evaluation

Use the current request, confirmed requirements, relevant conversation, and minimum necessary read-only context. Assess:

- Clarity of scope and acceptance criteria
- Required judgment, unfamiliarity, and reasoning difficulty
- Consequences and reversibility of mistakes
- Strength of independent verification
- Dependencies and context that must remain coherent
- Relevant failures and the user's quality, time, or usage priorities

Many files, a long task, or a high-risk keyword alone does not determine the configuration. Judge the actual decisions and consequences.

## Candidate Configurations

Consider all available combinations of these four models and five reasoning levels. Do not restrict each model to its usual starting level or force variety between recommendations.

| Model | Selection basis |
| --- | --- |
| GPT-5.6 Luna | Explicit, bounded work with established methods and reliable checks: mechanical edits, focused fixes, transformations, repeatable tasks, or implementation from a precise plan. |
| GPT-5.6 Terra | Everyday implementation, integrations, refactoring, and debugging requiring moderate judgment within understandable dependencies. |
| GPT-5.6 Sol | Complex or open-ended work requiring substantial analysis, design judgment, difficult diagnosis, or careful synthesis. |
| GPT-6 Astra | Demanding end-to-end work requiring sustained judgment across systems, tools, changing constraints, or long context; difficult tasks where improved overall understanding and follow-through matter. |

These are routing guidelines, not measured rankings for every task and effort combination. Sol remains a candidate when it meets the reliability requirement; Astra need not wait for Sol to fail when the initial workload already justifies it.

Use only configurations confirmed available in the current client. If availability is uncertain, disclose it and resolve it before giving a definitive recommendation. API support does not prove that a client or account exposes the same option.

## Reasoning Levels

Choose effort relative to the selected model and the work remaining.

| Output label | Effort | When to consider it |
| --- | --- | --- |
| 轻度 | low | The approach is clear and limited exploration is needed, even if strong model judgment is useful. |
| 中 | medium | Ordinary planning, implementation decisions, and verification; a useful baseline when effort needs are uncertain. |
| 高 | high | Several plausible hypotheses, interacting edge cases, cross-file reasoning, or substantial checking. |
| 极高 | xhigh | Deeply interacting uncertainties, difficult state or architecture reasoning, and extensive hypothesis testing. |
| 更高（消耗更多使用额度） | max | Extended exploration is likely to materially improve a particularly difficult result beyond xhigh. |

Effort is not a universal intelligence score or a fixed token budget. Higher effort is not guaranteed to improve correctness.

All twenty combinations remain candidates when available:

| Model | 轻度 | 中 | 高 | 极高 | Max |
| --- | --- | --- | --- | --- | --- |
| Luna | Direct transformations | Planned bounded changes | Bounded logic with edge cases | Deep but tightly specified reasoning | Exceptional bounded work with evidence that extra exploration helps |
| Terra | Familiar clear changes | Everyday engineering | Non-trivial debugging | Interacting implementation hypotheses | Difficult work within its demonstrated capability |
| Sol | Strong judgment with a clear approach | Complex implementation or synthesis | Difficult diagnosis or design | Deep architectural or state reasoning | Exceptional problems benefiting from extended analysis |
| Astra | Strong overall understanding with limited exploration | Demanding multi-stage execution | Complex cross-system diagnosis and verification | Deep uncertainty across systems and context | Hardest end-to-end work benefiting from maximum exploration |

These cells are candidate use cases, not mandatory assignments or benchmark results. Do not automatically discard Luna or Terra at high effort, or Sol or Astra at low effort. Select them only when their combination fits the task.

## Selection Procedure

1. Establish the required correctness and reliability from the task's consequences and checks.
2. Choose a model candidate for the required understanding, judgment, and sustained coherence.
3. Choose effort for the remaining exploration and verification.
4. Compare plausible alternatives, including a smaller model with more effort and a stronger model with less effort. Decide using task fit and relevant evidence.
5. Among configurations expected to meet the reliability requirement, respect the user's priorities and prefer lower expected total usage when reasonably supported. If usage is unknown, do not invent a cheapest option.
6. Return one configuration and a brief task-specific reason.

Do not assume fixed cross-model equivalence, such as Astra low = Luna high, or that a higher-tier model at low always beats a lower-tier model at max.

Upgrade the model when evidence points to misunderstanding, poor judgment, or loss of task coherence. Increase effort when the model understands the work but needs deeper exploration. Missing requirements, permissions, unavailable tools, or broken environments are not solved by changing models.

## Usage and Execution Modes

Distinguish token count, price or credits per token, and total usage to reach a verified result. Include relevant input, cached input, output and reasoning, tool loops, and retries without double-counting reasoning already included in output totals.

Fewer tokens do not necessarily mean fewer credits. Lower token rates do not guarantee a cheaper completed task. Do not infer exact savings or token counts from model names or effort labels; use current rates and comparable task evidence when needed.

Ultra is a separate delegation mode, not an ordinary sixth reasoning depth. Consider it only when available and parallel work is authorized and useful for independent subtasks. Do not enable it or create agents as part of Decision. The standard recommendation remains one model and one of the five effort levels; discuss a user-requested execution mode before that line.

## Output and Confirmation

Give the short explanation or clarification required by the task, identifying the main selection factor. Do not turn Decision into another planning phase.

The final line MUST contain exactly one model and one reasoning level:

`<recommended model>，思考等级<recommended reasoning level>`

Use plain text without a heading, code block, or any content after the recommendation. Stop and wait for confirmation; do not execute in the same response.

The user manually applies the configuration and authorizes execution. Do not claim the settings changed without confirmation.

The recommendation stays valid while the work remains materially unchanged. Re-evaluate when requirements, risk, verification, context, available configurations, or relevant capability-failure evidence materially change. Routine continuation does not require repeated confirmation.
