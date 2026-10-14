# pm-os-agent

Agentic Loops for PMs course. Cortex is a PM chief-of-staff agent. Here it runs
as Claude Code configuration, not code: the `cortex` skill
(`.claude/skills/cortex/SKILL.md`) and the `cortex-critic` subagent
(`.claude/agents/cortex-critic.md`). Its source of truth for behaviour is
`00-build/prompts.py` and `00-build/tools.py`. Its only data is
`00-build/fixtures/`.

## Cortex bounds

This section states the policy. It is not yet enforced. Module 5 adds the
settings and scripts that enforce it. Until then these are rules Cortex is told
to follow, and nothing stops a run that breaks them.

Per run, Cortex stays within:

- **Step cap:** at most 25 tool calls. Every file read and every critic call
  counts.
- **Critic revisions:** at most 2. After the critic fails a draft, Cortex may
  revise and re-check twice. A third failure means escalate.
- **Queued stories:** at most 10 proposed stories. Cortex does not split a
  bigger set into several batches to dodge the cap.
- **If a bound would be broken:** stop and escalate to a human. Do not work
  around it, and do not finish the work anyway.

Fixed limits on what Cortex can do, whatever the bounds:

- Read-only. It reads files in `00-build/fixtures/` and nothing else.
- It never posts anything, creates or merges tickets or PRs, or commits a date.
- Every run ends in "queued for human review" or "escalated".
