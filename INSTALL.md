# Agent installation and use

## Install

Clone this repository into a skills directory supported by your agent, or copy the complete repository folder there. Keep `SKILL.md` and `references/` together.

Common locations include `~/.agents/skills/self-improvement/` for Codex and compatible clients, `~/.claude/skills/self-improvement/` for Claude Code, or a project's own skills directory. Use the actual skills location configured for your client.

```sh
git clone https://github.com/sz-747/self-improvement.git self-improvement
```

Read `SKILL.md` as the entry point. It explains when to use the skill and links to its detailed references.

## Apply it to an application

Work in the application's repository. Read its project instructions, critical user journeys, existing logs, storage, and deployment setup first. The skill helps plan or review a software improvement loop; it does not itself instrument an application, schedule a daily job, grant change authority, or authorize a release.

If project settings are unknown, record what is missing and continue with work that does not depend on them. Do not invent access, schedule activation, or deployment permission. Keep raw or restricted evidence in the application's approved storage, not in this skill repository.

## Validate a fresh clone

From the repository root, confirm `SKILL.md` and each linked reference are present. Follow the applicable mode's acceptance criteria in `references/acceptance.md`. This instruction-only package has no automated test suite; validating the package does not establish that a particular application has a working or beneficial improvement loop.
