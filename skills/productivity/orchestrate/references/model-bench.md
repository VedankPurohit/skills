# Model Bench

Use this reference only when the runtime lets the orchestrator choose a model. Availability beats preference. Treat the role as the durable rule and model names as current examples. Model catalogs, prices, subscriptions, aliases, and reasoning controls change; inspect the current runtime before routing.

## Route by role

| Role | Prefer when available | Use for |
| --- | --- | --- |
| Frontier arbiter | Claude Fable 5; GPT-5.6 Sol | High-stakes judgment, difficult synthesis, architecture disputes, explicit quality-first review |
| Deep specialist | Claude Opus; GPT-5.6 Sol or Terra; current frontier GPT | Complex coding, research, diagnosis, security and correctness analysis |
| Default worker | Claude Sonnet; GPT-5.6 Terra | Substantial coding, ordinary research, focused review, implementation |
| Exploration worker | GPT-5.6 Luna; Claude Sonnet | Breadth-first exploration, repository mapping, independent hypotheses |
| Economy worker | GPT-5.6 Luna; Claude Haiku; current small model | Text processing, mechanical checks, narrow searches, classification, simple isolated work |

Treat family names such as Opus, Sonnet, and Haiku as aliases only when the current provider exposes them. Prefer a current-generation model. Use a previous generation only when the current generation is unavailable, a compatibility or evaluation constraint requires it, or the user asks for it.

## Route specialized work

- **UI, UX, and frontend design:** Prefer Claude Fable or the current Claude Opus when an authorized Claude worker is actually available, including when the root runtime is Codex. Use the best available current-generation model otherwise. Keep implementation and verification on whichever workers have the necessary repository and browser tools.
- **Computer use and browser operation:** Prefer GPT-5.6 Sol when available. Use GPT-5.6 Terra for routine form filling, dashboard inspection, application testing, or visual verification when Sol is unnecessary or unavailable. Fall back to the best tool-capable current-generation model.
- **High-volume text processing:** Prefer GPT-5.6 Luna at medium reasoning. Use high only when the branch needs judgment beyond extraction, transformation, classification, or summarization. Fall back to Claude Haiku, then another available economy model.
- **Complex coding and research:** Prefer the balanced or deep-specialist tier. Escalate only the branches whose difficulty justifies it.

## Match shape to model

- Use frontier models sparingly for branches where a marginal reasoning gain changes the outcome.
- Use balanced models for most implementation and research contracts.
- Use Luna freely for many narrow, independent, checkable text branches, bounded by real task partitions and the runtime concurrency limit. Require evidence and verify the fan-in.
- Prefer a different provider or model family for a tie-breaker when correlated blind spots matter.
- Default reasoning effort to medium. Use high for difficult branches with a clear quality benefit.
- Avoid xhigh, max, ultra, or equivalent settings unless the user explicitly requests them or a concrete, high-stakes branch has already failed at high. Do not equate maximum effort with better orchestration.

## Review ensembles

For an explicit thorough review, assign distinct axes rather than repeating the same generic prompt. A useful set is:

1. correctness and edge cases;
2. security and abuse paths;
3. performance and reliability;
4. maintainability and architecture;
5. specification and user-intent fidelity.

Use three to five axes according to risk. Prefer frontier or deep-specialist models for the highest-risk axes and balanced or exploration models for the rest. The orchestrator deduplicates findings, checks the diff or evidence, and ranks only substantiated issues.

## Cost discipline

"Cheap" is relative to the user's account. Subscription quotas, API billing, promotions, and host-level credits differ. Treat Luna as the preferred economy worker when it is listed, but never promise that any model is free. Do not launch a paid external provider merely because its CLI is installed.
