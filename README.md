# New Project Harness

A [Pi](https://pi.dev) skill that helps set up new or existing software projects for reliable
coding-agent work. It adapts a small set of project templates to the repository instead of blindly
copying generic setup commands.

## What it creates

When you ask the skill to bootstrap a project, it inspects the repository and creates or updates:

- `AGENTS.md` — project instructions, startup steps, scope rules, and definition of done
- `feature-list.json` — a structured list of features, dependencies, status, and verification evidence
- `init.sh` — project-specific setup and verification commands
- `progress.md` — a record of current project and session state
- `session-handoff.md` — context and next steps for the next session

The skill asks about important unknown requirements or architecture choices. It preserves existing
files and user changes. It also includes preferences for using `mise` when applicable and writing
user-facing prose in ASD-STE100 Simplified Technical English by default.

## Install with Pi

Install from this Git repository:

```bash
pi install git:github.com/jochalek/pi-new-project-harness
```

To pin an install to a release tag, add the tag after `@`, for example:

```bash
pi install git:github.com/jochalek/pi-new-project-harness@v1.0.0
```

Pi loads the skill from the package. In a running Pi session, use `/reload` after installation if
needed. To invoke it explicitly, run:

```text
/skill:new-project-harness
```

You can also ask naturally, for example: “Set up this project for agent work.” The skill is useful
for initializing a new project or adding a harness to an existing repository.

## Use without installing a package

Copy the `new-project-harness` skill directory into one of Pi's skill locations, such as:

```text
~/.pi/agent/skills/new-project-harness/
```

Keep `SKILL.md` and the `templates/` directory together. Pi discovers the skill from its
`SKILL.md` file.

## Repository layout

```text
new-project-harness/
├── package.json
├── README.md
├── SKILL.md
└── templates/
    ├── agents.md
    ├── feature-list.json
    ├── init.sh
    ├── progress.md
    └── session-handoff.md
```

The templates are based on the [Walking Labs harness-creator templates](https://github.com/walkinglabs/learn-harness-engineering/tree/main/skills/harness-creator/templates).
The skill adapts them to project facts and requirements. It does not run dependency installation or
other setup with side effects without user approval.
