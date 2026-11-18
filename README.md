# Skills

Reusable agent skills by Samuel Söderberg.

| Skill | When to use it |
| --- | --- |
| [disinfect](skills/disinfect/SKILL.md) | After a change settles, remove leftover scaffolding, dead fallbacks, and abandoned designs. |
| [overnight-analysis](skills/overnight-analysis/SKILL.md) | Work until a deadline, finish the task early, then use the remaining time for deeper checks. |

## Install

```sh
npx skills add sasoder/skills
```

Choose the skills and agents to install to. To install just one:

```sh
npx skills add sasoder/skills --skill disinfect
```

Add `-g` to install across projects. These skills use the [Agent Skills format](https://agentskills.io/specification) and contain no project-specific commands or services.

## Use

Ask your agent to use the skill by name. In Codex, for example:

```text
Use $disinfect to clean up the finished change.
Use $overnight-analysis to investigate this until 09:00 tomorrow, in my timezone.
```

`disinfect` reviews the change and its immediate callers and callees. It preserves external contracts and verifies its cleanup.

`overnight-analysis` keeps a state file and checkpoints every 30 minutes. Unattended execution depends on the host's ability to keep working or resume the session. The skill does not grant extra permissions or spending approval.

## License

[MIT](LICENSE).
