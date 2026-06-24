# kylinos-v11-desktop-enhance-skill

[中文](README.md)

This repository is a structured feature-enhancement knowledge base for KylinOS Desktop V11. It records reusable workflows for desktop-system capabilities that already work but need new behavior, changed defaults, local customization, or source-level enhancement. It is not an executable program and is not tied to one AI tool's built-in skill directory. Humans can browse the directories directly, and multiple AI tools can start from `$HOME/.os-enhance-skill/SKILL.md` and progressively load only the relevant references.

It currently covers UKUI global search, search engines, custom commands, tray status badges, AI-tool global prompts, Codex user-level configuration, DATA workspaces, local source customization, source patch preservation, build workflows, and rollback strategy.

Existing behavior failures, errors, broken persistence, installation failures, or damaged system services belong in `$HOME/.os-fix-skill`.

## Install an AI Coding Tool First

If you do not already have an AI coding tool, install one of Codex, Claude Code, or opencode first. The commands below target KylinOS Desktop V11 and similar Linux desktop terminals. For more installation methods, use the linked official docs.

### Codex

Official docs:

- Codex CLI: https://developers.openai.com/codex/cli
- Codex quickstart: https://developers.openai.com/codex/quickstart

Recommended install command:

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Start it with:

```bash
codex
```

### Claude Code

Official docs:

- Claude Code quickstart: https://docs.anthropic.com/en/docs/claude-code/quickstart
- Claude Code setup: https://docs.anthropic.com/en/docs/claude-code/setup

Recommended install command:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Start it with:

```bash
claude
```

### opencode

Official docs:

- opencode docs: https://opencode.ai/docs/
- opencode download: https://opencode.ai/download

Recommended install command:

```bash
curl -fsSL https://opencode.ai/install | bash
```

Start it with:

```bash
opencode
```

If your system policy does not allow `curl | sh` or `curl | bash`, open the official pages above and choose a standalone package, npm, or another trusted installation method for your Linux desktop environment.

## Install The System Knowledge Bases

### Option 1: Ask an AI Tool to Install It

Send this prompt to Codex, Claude Code, opencode, or a similar tool:

```text
Please install these KylinOS Desktop V11 system knowledge bases:

- Repair knowledge base: https://github.com/Swordup-Z/kylinos-v11-desktop-fix-skill
- Feature-enhancement knowledge base: https://github.com/Swordup-Z/kylinos-v11-desktop-enhance-skill

Requirements:
1. Clone the repair knowledge base to $HOME/.os-fix-skill.
2. Clone the feature-enhancement knowledge base to $HOME/.os-enhance-skill.
3. Configure the user-level global prompt for the current tool, for example:
   - Codex: $HOME/.codex/AGENTS.md
   - Claude Code: $HOME/.claude/CLAUDE.md
   - opencode: $HOME/.config/opencode/AGENTS.md
4. When the user works on KylinOS Desktop V11, UKUI, KARE/Kaiming, Clash Verge, TUN, maintenance mode, the PanShi architecture, system services, partitions, mounts, or desktop AI subsystem repair issues, first read $HOME/.os-fix-skill/SKILL.md, then follow its references routing.
5. When the user works on feature enhancement, local customization, default-behavior changes, AI-tool configuration, UKUI behavior extension, application installation experience, network policy, storage strategy, hardware capability enhancement, or source-level feature enhancement, first read $HOME/.os-enhance-skill/SKILL.md, then follow its references routing.
6. When the user works under $HOME/desktop-develop or /data/usershare/desktop-develop on an independent tool/application, first read that directory's AGENTS.md and follow the workspace or project-level routing; do not put project implementation requirements into either skill.
7. After installation, tell me both entry file paths and how to use them later.
```

### Option 2: Manual Installation

```bash
cd "$HOME"
git clone https://github.com/Swordup-Z/kylinos-v11-desktop-fix-skill.git "$HOME/.os-fix-skill"
git clone https://github.com/Swordup-Z/kylinos-v11-desktop-enhance-skill.git "$HOME/.os-enhance-skill"
```

Entry files:

```text
Repair: $HOME/.os-fix-skill/SKILL.md
Enhancement: $HOME/.os-enhance-skill/SKILL.md
```

Common user-level prompt files:

```text
Codex:       $HOME/.codex/AGENTS.md
Claude Code: $HOME/.claude/CLAUDE.md
opencode:    $HOME/.config/opencode/AGENTS.md
```

Use a fixed session name for system enhancement, such as `os-enhance`:

```bash
codex resume os-enhance
claude resume os-enhance
opencode resume os-enhance
```

## Architecture

This skill only keeps system enhancement workflows: the system already works, but the user wants new capabilities, changed defaults, local customization, or reusable enhancement workflows. Examples include adding Bing/Google to UKUI global search, adding a custom command panel, adding tray input-method status badges, preserving local source patches, or configuring AI-tool global prompts.

Enhancement content is grouped by scenario:

```text
system
applications
ukui
network
hardware
storage
agent-tools
source-rebuild
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
└── README.en.md
```

`references/` is the scenario routing layer. Each reference contains scope, a short explanation, a knowledge entry, and minimal diagnostics. `knowledge/feature-enhancement/<scenario>/README.md` is the scenario index that routes to one concrete chapter. The concrete `<topic>.md` files contain background, pre-checks, enhancement steps, verification, rollback, and risk boundaries. Reusable source-level enhancements also keep patch sets and `PATCHSET.md` metadata under the same scenario's `patches/<feature-id>/` directory.

Fixed loading path:

```text
enhancement request
-> scenario reference
-> scenario knowledge README
-> concrete knowledge chapter
```

## Routing Examples

Configuring Codex, Claude Code, or opencode to load shared knowledge bases:

```text
SKILL.md
-> references/feature-enhancement/agent-tools.md
-> knowledge/feature-enhancement/agent-tools/README.md
-> knowledge/feature-enhancement/agent-tools/global-prompts.md
```

Adding a custom command panel to UKUI global search:

```text
SKILL.md
-> references/feature-enhancement/ukui.md
-> knowledge/feature-enhancement/ukui/README.md
-> knowledge/feature-enhancement/ukui/search-command-provider.md
```

Adding Bing/Google search engines to UKUI global search:

```text
SKILL.md
-> references/feature-enhancement/ukui.md
-> knowledge/feature-enhancement/ukui/README.md
-> knowledge/feature-enhancement/ukui/search-web-engine.md
```

Planning a DATA-partition local source customization workspace:

```text
SKILL.md
-> references/feature-enhancement/source-rebuild.md
-> knowledge/feature-enhancement/source-rebuild/README.md
-> knowledge/feature-enhancement/source-rebuild/local-customization-index.md
```

For repair tasks such as TUN failures, autostart not working, global-search errors, desktop AI residues, or damaged services, use `$HOME/.os-fix-skill/SKILL.md`.

## Coverage

- AI-tool global prompts, Codex user-level configuration, full-access permission boundaries, and multi-tool loading rules.
- UKUI global-search search-engine customization.
- UKUI global-search custom command provider and graphical command configuration.
- UKUI system-tray input-method status badges and similar desktop interaction enhancements.
- Local source customization workspaces, commits, patches, and build-artifact cleanup.
- Reusable source patch sets, upstream repositories, base nodes, and conflict migration rules.
- DATA partition layout for local source, builds, rollback packages, and development work.
- Extensible categories for application installation experience, desktop entries, user-level installation flows, network policy, and hardware capability enhancement.

## Safety Boundary

System-level enhancements on KylinOS Desktop V11 often require maintenance mode. Before touching `/usr`, `/etc`, `/opt`, system packages, systemd units, device nodes, partitions, KSaf, or system services, check:

```bash
mm-cli -s
```

Enter maintenance mode:

```bash
sudo mm-cli -o
```

Exit and save:

```bash
sudo mm-cli -c -a
```

Switching maintenance mode usually requires a reboot. Detailed operational rules live in `SKILL.md` and the relevant reference/knowledge chapters.

Enhancement plans should prefer user-level configuration, reversible configuration, and least-privilege paths. When source-level patches or system-file replacement are necessary, record pre-checks, impact scope, rollback, and verification steps.

## Companion Tools

Space cleanup, Kaiming/KARE layer control, ostree usage auditing, and desktop automation should live in companion applications instead of large embedded scripts or project-specific development requirements inside knowledge files. If a local development workspace exists, read the workspace prompt first:

```text
$HOME/desktop-develop/AGENTS.md
```

This skill keeps only enhancement strategy, safety boundaries, and reusable knowledge. Concrete UI, build, verification, dependency, and implementation rules belong in independent projects. Tool projects must still follow the system safety boundary: do not automatically delete ostree deployments, EFI files, GRUB config, loader entries, `/etc/fstab`, or partition tables.

On this machine, the usual development workspace entry is:

```text
$HOME/desktop-develop/AGENTS.md
```

That file only routes requests to projects; each concrete project continues from its own `AGENTS.md`.

## License

MIT License. See [LICENSE](LICENSE).
