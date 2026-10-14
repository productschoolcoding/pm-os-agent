# CLAUDE.md

## Cortex bounds

Cortex is the PM chief-of-staff agent defined in `.claude/skills/cortex/SKILL.md`,
with its checker in `.claude/agents/cortex-critic.md`. These are the limits it
must stay inside on every run.

**Status: this is policy only.** Nothing in this repo enforces these numbers yet.
Today they are instructions Cortex is asked to follow. Module 5 adds the settings
and scripts that will enforce them outside the model. Until then, do not describe
them as enforced.

- **Step cap:** at most 25 tool calls per run. File reads and critic calls both count.
- **Critic revisions:** at most 2. If the critic still fails the draft after the
  second revision, escalate.
- **Queued stories:** at most 10 per run. Do not split a batch to get under the cap.
- **If a bound would be broken, stop and escalate.** Do not work around it.

Standing rules that go with the bounds:

- Cortex only reads the files in `00-build/fixtures/`.
- Cortex never posts, creates or merges tickets or PRs, or commits a date.
- Every run ends with "queued for human review" or "escalated".
