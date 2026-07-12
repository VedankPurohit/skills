---
name: orchestrate
description: Orchestrate substantial coding, research, exploration, and review by decomposing work into bounded parallel agents, choosing available models by difficulty and cost, and synthesizing verified results. Use when a task has multiple independent workstreams, benefits from competing perspectives or specialist context, or explicitly calls for a thorough multi-angle review. Skip for trivial, tightly sequential, or coordination-heavy work.
---

# Orchestrate

Act as the manager. Own the goal, decomposition, boundaries, synthesis, verification, and user communication. Delegate execution when doing so materially improves speed, coverage, or independent judgment.

## 1. Identify yourself and inventory the bench

Identify the current agent runtime and root model from system-provided metadata. Determine whether you are running as Codex, Claude Code, another agent, or an unidentified runtime. Then inspect the collaboration, task, and model-selection capabilities actually exposed to this run.

- Do not guess your identity from the repository, skill text, or installed software.
- Treat a model as available only when the current callable agent surface lists it or an already-authorized provider exposes it through a non-billing capability listing.
- Never infer entitlement from an installed CLI, an auth or config file, a subscription guess, or a model name in this skill. Do not inspect credentials.
- Never spend a model call merely to test access. If a model selected from an authoritative listing still returns an availability error, fall back once to the closest listed tier.
- Do not assume that a Codex runtime can call Claude, or that a Claude runtime can call Codex. Use cross-provider workers only through a capability explicitly available and authorized in the current run.
- Use internal subagents by default. Create visible, user-owned tasks or threads only when the user explicitly asks for them.
- If model choice is unsupported, delegate using the runtime default. If delegation itself is unavailable, continue in the main agent.

When model choice is available, read [the model bench](references/model-bench.md) before assigning workers.

Completion criterion: know the root runtime when disclosed, which delegation surfaces are callable, which models those surfaces actually expose, and which constraints apply.

## 2. Pass the delegation gate

Delegate when at least one condition holds:

- Two or more useful workstreams can proceed independently.
- A bounded specialist can inspect a distinct subsystem, source set, hypothesis, or review axis.
- Independent contexts or competing opinions reduce anchoring and materially improve confidence.
- The task is broad enough that parallel exploration saves meaningful wall-clock time.

Stay local when the task is small, tightly sequential, dominated by one shared write surface, or cheaper to complete than to specify and integrate. Parallelizable is not enough; the expected benefit must exceed coordination cost.

Completion criterion: either identify concrete independent workstreams or record the reason to continue locally.

## 3. Build the smallest useful team

Turn the work into a dependency-aware map. Spawn one worker per real branch, normally two to four. Do not create duplicate generalists unless independent replication is the point.

Scale beyond four only for a naturally sharded corpus, broad hypothesis search, or an explicitly exhaustive review. Cap the team by the number of independent branches and the runtime's concurrency limit, not by a fixed swarm target.

Choose the least expensive model likely to clear each branch's quality bar. Reserve frontier models for difficult synthesis, high-stakes judgment, architecture, security, or an explicit quality-first request.

For high-stakes, ambiguous, architectural, or explicitly thorough work, obtain one independent frontier opinion when available. Prefer a different model family from the primary worker to reduce correlated blind spots. Do not make this gate mandatory for routine work.

Completion criterion: every planned worker has a distinct reason to exist, and no dependency requires it to wait behind unfinished work presented as parallel.

## 4. Issue contracts, not vague prompts

Give each worker:

- one bounded objective;
- the minimum necessary context and inputs;
- explicit scope and authority boundaries;
- a required deliverable and evidence format;
- write ownership, or read-only status;
- a stopping condition.

Partition concurrent code edits by file or component. Never let workers edit the same files concurrently. Partition research by question, source class, or hypothesis. Partition review by named axes such as correctness, security, performance, maintainability, and specification fidelity.

Ask workers to report uncertainty, failed approaches, and conflicts instead of smoothing them away. Allow recursive delegation only when the runtime permits it and the new branches pass the same delegation gate.

Completion criterion: another agent can execute each contract without guessing its scope, output, or stopping point.

## 5. Fan out and manage

Launch independent contracts concurrently. Keep the main agent on management work: inspect shared constraints, prepare integration, track dependencies, and prevent duplicated effort.

Use follow-ups only to fill a concrete evidence gap, resolve a contradiction, or redirect drift. Do not repeatedly poll workers that can notify on completion. Do not redo delegated work in the main agent unless verification exposes a gap.

For side effects, preserve the user's authorization boundary. Delegation never grants broader permission than the original request.

Completion criterion: every required branch has either returned a usable result or has a documented failure that the main agent has handled.

## 6. Fan in and own the answer

Treat worker output as evidence, not truth.

1. Compare results against their contracts.
2. Trace important claims to files, tests, logs, or cited sources.
3. Reconcile disagreements explicitly; use a targeted tie-breaker only when the conflict is material.
4. Integrate changes in dependency order.
5. Run final validation at the combined-system level.
6. Communicate one coherent answer in the main agent's voice.

Do not dump worker transcripts on the user. Surface delegation details only when they explain confidence, tradeoffs, unresolved disagreement, or provenance.

Completion criterion: the integrated result meets the user's success criteria, material claims are supported, conflicts are resolved or disclosed, and the main agent can defend the final answer.
