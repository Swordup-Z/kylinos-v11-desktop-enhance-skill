# kylinos-v11-desktop-enhance-skill

[中文](README.md)

Verified enhancement workflows for KylinOS Desktop V11, including pre-checks, rollback notes, risk boundaries, and validation steps for desktop system improvements.

This repository is not an executable program and is not tied to a specific AI tool's built-in skill directory. It is a shared structured knowledge base for people and AI tools. AI tools should start from `$HOME/.os-enhance-skill/SKILL.md` and load only the matching references as needed.

## Scope

Use this repository when the system already works, but the user wants to add capability, change default behavior, or keep a reusable local customization workflow, such as:

- UKUI search, search engines, custom commands, tray behavior, shortcuts, and panel behavior.
- Application installation experience, desktop entries, and user-level installation flows.
- Network policy, proxy integration, and TUN usability improvements.
- DATA workspace, partition usage, local development space, and cleanup strategy.
- AI tool global prompts, permission boundaries, automatic skill loading, and desktop operation workflows.
- Source-level feature enhancements, local patch preservation, build steps, and rollback strategy.

If the issue is an existing behavior failure, error, broken persistence, installation failure, or damaged system service, use `$HOME/.os-fix-skill/SKILL.md` first.

## Install

```bash
cd "$HOME"
git clone https://github.com/Swordup-Z/kylinos-v11-desktop-enhance-skill.git "$HOME/.os-enhance-skill"
```

Entry point:

```text
$HOME/.os-enhance-skill/SKILL.md
```

Install the repair knowledge base as a companion so global prompts can route by task type:

```bash
git clone https://github.com/Swordup-Z/kylinos-v11-desktop-fix-skill.git "$HOME/.os-fix-skill"
```

## Suggested Global Prompt

Add this rule to your AI tool's user-level prompt, such as Codex `$HOME/.codex/AGENTS.md`, Claude Code `$HOME/.claude/CLAUDE.md`, or opencode `$HOME/.config/opencode/AGENTS.md`:

```text
When working on KylinOS Desktop V11 feature enhancement, local customization, default behavior changes, AI tool configuration, UKUI behavior extension, application installation experience, network policy, storage strategy, hardware capability enhancement, or source-level feature enhancement, read $HOME/.os-enhance-skill/SKILL.md first, then follow its references routing.

If the user describes an existing behavior failure, error, broken persistence, installation failure, or damaged system service, read $HOME/.os-fix-skill/SKILL.md first.
```

## Directory Layout

```text
$HOME/.os-enhance-skill/
├── SKILL.md
├── references/
│   ├── README.md
│   └── feature-enhancement/
│       ├── README.md
│       ├── system.md
│       ├── applications.md
│       ├── ukui.md
│       ├── network.md
│       ├── hardware.md
│       ├── storage.md
│       ├── agent-tools.md
│       └── source-rebuild.md
├── knowledge/
│   ├── README.md
│   └── feature-enhancement/
│       ├── agent-tools/
│       ├── applications/
│       ├── hardware/
│       ├── network/
│       ├── source-rebuild/
│       ├── storage/
│       ├── system/
│       └── ukui/
├── README.md
├── README.en.md
└── LICENSE
```

`references/` is the scenario routing layer. `knowledge/feature-enhancement/<scenario>/README.md` is the scenario index, and concrete `<topic>.md` files keep pre-checks, enhancement steps, verification, rollback, and risk boundaries. Source-level enhancement patches live under the matching scenario's `patches/<feature-id>/` directory with `PATCHSET.md` metadata.

## License

MIT
