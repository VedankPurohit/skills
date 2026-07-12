# Runtime Adapters

Read this reference only when launching a model-specific worker, selecting reasoning effort, or crossing provider boundaries. Models do not call one another directly; the surrounding runtime invokes another model through a tool, custom-agent definition, SDK, gateway, or CLI.

## Select the invocation surface

Use the first available route:

1. Native subagent tool whose schema exposes the required controls.
2. Native custom-agent definition with the model and effort pinned.
3. Already-configured, authorized cross-provider tool or gateway.
4. Non-interactive provider CLI only when the user authorized cross-provider usage and the CLI is an established worker surface.
5. Same-provider or runtime-default fallback.

Inspect the active tool schema before every route. Pass only fields the schema declares. If the spawn tool has no `model` or effort field, do not invent one; use a named custom agent or accept inheritance.

For CLI adapters, verify flags against the installed command's current `--help` output before use. The examples below show the intended controls, but provider CLIs evolve independently of this skill.

An installed executable, saved configuration, or auth file does not establish permission or entitlement. Do not inspect credentials and do not make a paid probe call. Cross-provider routing must be explicitly callable and authorized in the current run.

## Codex native agents

Define repeatable Codex workers under `.codex/agents/` for a project or `~/.codex/agents/` for a user. Pin the model and effort in TOML when per-invocation selection is unavailable:

```toml
name = "text_processor"
description = "Processes a bounded text batch and returns structured results."
model = "gpt-5.6-luna"
model_reasoning_effort = "medium"
sandbox_mode = "read-only"
developer_instructions = """
Return only the requested schema. Cite the source location for every extracted value.
"""
```

Spawn the named agent through the native collaboration surface. If `model` or `model_reasoning_effort` is omitted, Codex may choose or inherit them. Keep `agents.max_depth` at one unless recursive delegation has a concrete need.

## Claude Code native agents

Define repeatable Claude workers under `.claude/agents/` for a project or `~/.claude/agents/` for a user:

```markdown
---
name: ux-reviewer
description: Reviews one interface against a supplied UX contract
model: fable
effort: high
tools: Read, Glob, Grep
---

Return ranked findings with evidence. Do not edit files.
```

Claude Code accepts `fable`, `opus`, `sonnet`, `haiku`, a full Claude model ID, or `inherit`. Its Agent tool may also accept a per-invocation `model`; use it only when present in the live schema. Configure `effort` in the subagent definition. Extended thinking follows the parent session and has no independent per-subagent switch.

## Non-interactive CLI fallback

Treat CLI launches as separate agent sessions, not native child agents. Restrict their working directory, permissions, tools, persistence, and output. Pass untrusted or multiline task content through stdin or a fixed prompt file instead of interpolating it into shell syntax.

Codex read-only worker:

```bash
codex exec \
  --model gpt-5.6-terra \
  -c model_reasoning_effort=medium \
  --sandbox read-only \
  --ephemeral \
  --cd /absolute/workspace \
  -
```

Claude Code read-only worker:

```bash
claude -p \
  --model sonnet \
  --effort medium \
  --permission-mode plan \
  --tools Read Glob Grep \
  --output-format json \
  --no-session-persistence \
  < /absolute/prompt.txt
```

Use medium effort by default and high for difficult judgment. Pass xhigh, max, ultra, or equivalents only under the escalation rule in the model bench. Never use sandbox-bypass or permission-bypass flags as an orchestration convenience.

## Cross-provider calls

A Claude root can reach a GPT worker only through an authorized Codex, OpenAI API, SDK, MCP, or gateway adapter. A Codex root can reach a Claude worker only through an authorized Claude API, Agent SDK, MCP, gateway, or approved CLI adapter. Naming the target model in a prompt does not create that bridge.

For every cross-provider call:

1. Verify the adapter is already exposed and permitted.
2. Verify its live model allowlist contains the target.
3. Set the model and effort using that adapter's actual field names.
4. Constrain tools and side effects to the worker contract.
5. Request a structured result with evidence and uncertainty.
6. Capture failure without retrying across models repeatedly.
7. Fall back to the closest available same-provider role when the bridge is absent or rejects the model.

The orchestrator remains responsible for validating and synthesizing the returned result.
