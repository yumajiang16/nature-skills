# Nature Skills in Codex

Project skills are registered in `.agents/skills/` with relative symlinks to
`skills/`. Keep the links and their targets together; do not copy or edit a
second set of skill definitions. Use the existing checkout, without creating a
worktree unless the user requests one.

For scientific figures use `nature-figure`; for editing existing prose use
`nature-polishing`; for drafting from evidence use `nature-writing`; for
Nature/CNS supporting references use `nature-citation`. Read the selected
`SKILL.md`, its manifest, and the required routed resources before working.
`nature-shared` is a support package, not a standalone user workflow.

See [Codex project setup](docs/codex-project-skills.md) for installation,
runtime checks, invocation examples, and optional dependencies.

For Python tools in this cloud environment, activate
`/workspace/.venvs/nature-skills/bin/activate` when present. On another machine,
create a virtual environment and install the documented dependencies first.
Do not assume that background processes, API credentials, or a plotting backend
preference carry over between tasks. Honor the figure skill's Python/R choice
gate rather than silently selecting or saving a user preference.
