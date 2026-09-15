# Decision.md

Version: 3.1

## Purpose

Before implementation or any other state-changing action, recommend one model and one reasoning level, then stop and wait for the user's confirmation. The user applies the configuration manually; this file never switches models automatically.

Read-only discussion, research, review, or planning does not require the confirmation gate unless a model recommendation is requested. For a mixed request, complete the decision before the first state-changing phase.

## Default routing

Use the task's dominant phase. These are the normal defaults, not hard-coded equivalences or automatic settings.

| Task class | Default configuration | Examples |
| --- | --- | --- |
| Thinking, planning, and solution design | **GPT-6 Astra, high or above** | Requirement analysis, research synthesis, architecture, technical方案, trade-offs, risk analysis, task decomposition, test strategy, and other work where judgment determines the result. |
| Execution | **GPT-5.6 Luna, xhigh (极高)** | Writing or editing code, implementing an approved plan, refactoring, running or fixing tests, debugging, scripts, mechanical document edits, image generation/editing, and tool-driven production. |

For thinking tasks, use Astra `high` by default, `xhigh` when ambiguity, dependencies, or risk are substantial, and `max` only when extended exploration is likely to materially improve an unusually difficult result.

For execution tasks, use Luna `xhigh` by default. Use Luna `max` only when the bounded execution has evidence that extra exploration is worth the additional usage. Do not lower the default effort merely because the task looks short unless the user changes this policy.

If a request contains both planning and execution, split it into phases when possible: Astra `high` or above for the plan, then Luna `xhigh` for execution. Do not average the two phases into a made-up cross-model equivalence. If the phases cannot be separated, classify the dominant phase and explain the choice briefly.

GPT-5.6 Sol and GPT-5.6 Terra are not routine choices. Use them only when the user explicitly requests one, Astra or Luna is unavailable, or concrete compatibility/reliability evidence requires an exception. State the exception; never substitute silently.

## Decision procedure

1. Read the current request, confirmed requirements, and only the context needed for the upcoming action.
2. Classify the work as thinking/planning, execution, or mixed.
3. Assess ambiguity, judgment, consequences of error, dependencies, verification strength, and the user's quality or usage priorities.
4. Apply the default routing above, then adjust the reasoning level only when the task evidence supports it.
5. Confirm that the selected model and level are available in the current client. API availability alone is not proof of client or account availability.
6. Return one configuration and a short, task-specific reason. Do not implement, edit, or claim a setting change during this phase.

## Models and reasoning levels

Consider every available combination of these four models and five levels before choosing. The defaults above make Astra and Luna the normal path; they do not erase the other combinations from consideration.

| Model | Role in this policy |
| --- | --- |
| GPT-6 Astra (`gpt-6-astra`) | Primary model for thinking, planning, design, and difficult judgment. |
| GPT-5.6 Luna (`gpt-5.6-luna`) | Primary model for execution and clearly bounded production work. |
| GPT-5.6 Sol (`gpt-5.6-sol`) | Exception path for an explicitly requested or availability/compatibility-driven case. |
| GPT-5.6 Terra (`gpt-5.6-terra`) | Exception path for an explicitly requested or availability/compatibility-driven case. |

| Output label | API effort | Meaning |
| --- | --- | --- |
| 轻度 | `low` | Limited exploration; use only when the chosen task and model clearly support it. |
| 中 | `medium` | Ordinary exploration and checking. |
| 高 | `high` | Several plausible approaches, interacting edge cases, or substantial verification. |
| 极高 | `xhigh` | Deep uncertainty, difficult diagnosis, or extensive hypothesis testing. |
| 更高 | `max` | Maximum supported effort; reserve for exceptional cases where it is justified. |

These levels are relative to the selected model. They are not a universal intelligence scale, token budget, or price guarantee. Never assert a fixed equivalence such as “Astra low = Luna high.” A stronger model at low effort is not automatically better than a smaller model at xhigh, and a higher effort is not automatically more correct.

## Usage and special modes

Reasoning effort, token count, price/credits per token, and total usage to reach a verified result are different things. Do not invent exact token savings from a model name or effort label.

`Ultra` is a separate delegation mode, not a sixth reasoning level. Do not enable it or create agents as part of this decision; discuss it only when the user explicitly requests parallel, independent work and the client supports it.

## Output and confirmation

Give a concise reason tied to the task's dominant phase and risk. The final line must contain exactly one model and one reasoning level, with no heading or text after it:

`<recommended model>，思考等级<recommended reasoning level>`

Stop and wait for confirmation. Re-evaluate when the task, risk, verification, available configurations, or relevant failure evidence materially changes.
