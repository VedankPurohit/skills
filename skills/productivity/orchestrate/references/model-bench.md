# Model Bench

Use this reference only when the runtime lets the orchestrator choose a model. Availability beats preference. Model catalogs, prices, subscriptions, aliases, and reasoning controls change; inspect the current runtime before routing.

## Route by role

| Role | Prefer when available | Use for |
| --- | --- | --- |
| Frontier arbiter | Claude Fable 5; GPT-5.6 Sol | High-stakes judgment, difficult synthesis, architecture disputes, explicit quality-first review |
| Deep specialist | Claude Opus; GPT-5.6 Sol or Terra; current frontier GPT | Complex coding, research, diagnosis, security and correctness analysis |
| Default worker | Claude Sonnet; GPT-5.6 Terra | Substantial coding, ordinary research, focused review, implementation |
| Exploration worker | GPT-5.6 Luna; Claude Sonnet | Breadth-first exploration, repository mapping, independent hypotheses |
| Economy worker | GPT-5.4 Mini; Claude Haiku; current small model | Mechanical checks, narrow searches, classification, simple isolated work |

Treat family names such as Opus, Sonnet, and Haiku as aliases only when the current provider exposes them. Prefer the newest available member unless the user pins a version.

## Match shape to model

- Use frontier models sparingly for branches where a marginal reasoning gain changes the outcome.
- Use balanced models for most implementation and research contracts.
- Use fast models for many narrow, checkable branches; require evidence and verify their fan-in.
- Prefer a different provider or model family for a tie-breaker when correlated blind spots matter.
- Increase reasoning effort before escalating model tier only when the runtime supports it and the branch benefits from deeper reasoning.

## Review ensembles

For an explicit thorough review, assign distinct axes rather than repeating the same generic prompt. A useful set is:

1. correctness and edge cases;
2. security and abuse paths;
3. performance and reliability;
4. maintainability and architecture;
5. specification and user-intent fidelity.

Use three to five axes according to risk. Prefer frontier or deep-specialist models for the highest-risk axes and balanced or exploration models for the rest. The orchestrator deduplicates findings, checks the diff or evidence, and ranks only substantiated issues.

## Cost discipline

"Cheap" is relative to the user's account. Subscription quotas, API billing, promotions, and host-level credits differ. Use economy, balanced, and frontier as routing classes; never promise that a model is free. Do not launch a paid external provider merely because its CLI is installed.
