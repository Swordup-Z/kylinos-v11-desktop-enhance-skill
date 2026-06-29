# kylinos-v11-desktop-enhance-skill

[中文](README.md)

This repository is a structured feature-enhancement knowledge base for KylinOS Desktop V11. It records reusable workflows for desktop-system capabilities that already work but need new behavior, changed defaults, local customization, or source-level enhancement. It is not an executable program and is not tied to one tool's built-in directory. The entry file is `$HOME/.os-enhance-skill/SKILL.md`; detailed content is organized under `references/` and `knowledge/`.

It covers UKUI global search, search engines, custom commands, tray status badges, tool global rules, Codex user-level configuration, DATA workspaces, local source customization, source patch preservation, build workflows, and rollback strategy.

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

## Install This Knowledge Base

### Install by Pasting a Prompt into an AI Tool

Paste the following prompt into Codex, Claude Code, or opencode and let the AI tool install and connect this knowledge base for you:

```text
Please install the KylinOS Desktop V11 enhancement knowledge base kylinos-v11-desktop-enhance-skill on this machine and connect it to the current AI tool's user-level rule file.

Requirements:
1. Check that git is available first.
2. If $HOME/.os-enhance-skill does not exist, run:
   git clone https://github.com/Swordup-Z/kylinos-v11-desktop-enhance-skill.git "$HOME/.os-enhance-skill"
3. If $HOME/.os-enhance-skill already exists and is a git repository, only use non-destructive updates:
   git -C "$HOME/.os-enhance-skill" status -sb
   git -C "$HOME/.os-enhance-skill" fetch --prune
   git -C "$HOME/.os-enhance-skill" pull --ff-only
   If there are local changes, branch divergence, or a fast-forward failure, do not overwrite anything; report the reason instead.
4. If $HOME/.os-enhance-skill already exists but is not a git repository, do not delete or overwrite it; stop and explain why.
5. Confirm that $HOME/.os-enhance-skill/SKILL.md exists.
6. Create the parent directory for the current AI tool's user-level rule file if needed.
7. Append the rules below to the current AI tool's user-level rule file. If you cannot identify the current tool, ask me first. Do not overwrite existing content, and do not append duplicate rules if equivalent rules already exist.

Rule file locations:
- Codex: $HOME/.codex/AGENTS.md
- Claude Code: $HOME/.claude/CLAUDE.md
- opencode: $HOME/.config/opencode/AGENTS.md

Rules to append:
When the user is working on KylinOS Desktop V11 feature enhancement, local customization, default-behavior changes, AI tool configuration, UKUI behavior extensions, application installation experience, network policy, storage policy, hardware capability enhancement, or source-level feature enhancement, and the system already works but needs new capability, changed default behavior, or a reusable enhancement workflow, use $HOME/.os-enhance-skill/SKILL.md as the default knowledge entry. Before handling a system enhancement task, read $HOME/.os-enhance-skill/SKILL.md, then follow its reference routing and selectively read references/<scenario>.md. Then read only the referenced knowledge/<scenario>/README.md and one concrete knowledge chapter that matches the current goal. If no concrete reference or knowledge chapter matches, do not traverse the whole skill. Only read $HOME/.os-enhance-skill/references/system.md when the goal is clearly about maintenance workflow, persistence strategy, or general local-customization rules. Follow "diagnose the requirement and impact first, design the enhancement second, verify and record rollback last". Before any system-level enhancement involving /usr, /etc, /opt, system packages, system services, device nodes, partitions, KSaf policies, or similar system paths, run mm-cli -s to check maintenance mode; only modify system paths, system services, or system packages after confirming the machine is in maintain mode.

When finished, tell me the repository path, the rule file path you updated, and whether any update was skipped because of local changes or branch state.
```

### Manual Install

Clone or update this knowledge base first. Do not overwrite local changes in an existing directory. If `git pull --ff-only` fails, resolve the branch state before continuing.

```bash
if [ ! -d "$HOME/.os-enhance-skill/.git" ]; then
  git clone https://github.com/Swordup-Z/kylinos-v11-desktop-enhance-skill.git "$HOME/.os-enhance-skill"
else
  git -C "$HOME/.os-enhance-skill" status -sb
  git -C "$HOME/.os-enhance-skill" fetch --prune
  git -C "$HOME/.os-enhance-skill" pull --ff-only
fi
```

Entry file:

```text
$HOME/.os-enhance-skill/SKILL.md
```

Choose the user-level rule file for the current AI tool. Create its parent directory first if needed:

```text
Codex:       $HOME/.codex/AGENTS.md
Claude Code: $HOME/.claude/CLAUDE.md
opencode:    $HOME/.config/opencode/AGENTS.md
```

For Codex, for example:

```bash
mkdir -p "$HOME/.codex"
${EDITOR:-vi} "$HOME/.codex/AGENTS.md"
```

Append the following rules to the end of the selected rule file. Do not overwrite existing content, and do not append duplicates if equivalent rules already exist.

```text
When the user is working on KylinOS Desktop V11 feature enhancement, local customization, default-behavior changes, AI tool configuration, UKUI behavior extensions, application installation experience, network policy, storage policy, hardware capability enhancement, or source-level feature enhancement, and the system already works but needs new capability, changed default behavior, or a reusable enhancement workflow, use $HOME/.os-enhance-skill/SKILL.md as the default knowledge entry.

Before handling a system enhancement task, read $HOME/.os-enhance-skill/SKILL.md, then follow its reference routing and selectively read references/<scenario>.md. Then read only the referenced knowledge/<scenario>/README.md and one concrete knowledge chapter that matches the current goal. If no concrete reference or knowledge chapter matches, do not traverse the whole skill. Only read $HOME/.os-enhance-skill/references/system.md when the goal is clearly about maintenance workflow, persistence strategy, or general local-customization rules.

Follow "diagnose the requirement and impact first, design the enhancement second, verify and record rollback last". Before any system-level enhancement involving /usr, /etc, /opt, system packages, system services, device nodes, partitions, KSaf policies, or similar system paths, run mm-cli -s to check maintenance mode; only modify system paths, system services, or system packages after confirming the machine is in maintain mode.
```

After configuration, KylinOS Desktop V11 feature enhancement, local customization, default-behavior changes, tool configuration, or source-level feature work can start from `$HOME/.os-enhance-skill/SKILL.md` and then follow `references/`. System repair issues are maintained in `$HOME/.os-fix-skill`.

Use a fixed session name for system enhancement, such as `os-enhance`:

```bash
codex resume os-enhance
claude resume os-enhance
opencode resume os-enhance
```

## Architecture

This repository focuses on system enhancement workflows: the system already works, but the user wants new capabilities, changed defaults, local customization, or reusable enhancement workflows. Examples include adding Bing/Google to UKUI global search, adding a custom command panel, adding tray input-method status badges, preserving local source patches, or configuring tool global rules.

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
│   ├── system.md
│   ├── applications.md
│   ├── ukui.md
│   ├── network.md
│   ├── hardware.md
│   ├── storage.md
│   ├── agent-tools.md
│   └── source-rebuild.md
├── knowledge/
│   ├── README.md
│   ├── agent-tools/
│   ├── applications/
│   ├── hardware/
│   ├── network/
│   ├── source-rebuild/
│   ├── storage/
│   ├── system/
│   └── ukui/
├── README.md
└── README.en.md
```

`references/` is the scenario routing layer. Each reference contains scope, a short explanation, a knowledge entry, and minimal diagnostics. `knowledge/<scenario>/README.md` is the scenario index that routes to one concrete chapter. The concrete `<topic>.md` files contain background, pre-checks, enhancement steps, verification, rollback, and risk boundaries. Reusable source-level enhancements also keep patch sets and `PATCHSET.md` metadata under the same scenario's `patches/<feature-id>/` directory.

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
-> references/agent-tools.md
-> knowledge/agent-tools/README.md
-> knowledge/agent-tools/global-prompts.md
```

Adding a custom command panel to UKUI global search:

```text
SKILL.md
-> references/ukui.md
-> knowledge/ukui/README.md
-> knowledge/ukui/search-command-provider.md
```

Adding Bing/Google search engines to UKUI global search:

```text
SKILL.md
-> references/ukui.md
-> knowledge/ukui/README.md
-> knowledge/ukui/search-web-engine.md
```

Planning a DATA-partition local source customization workspace:

```text
SKILL.md
-> references/source-rebuild.md
-> knowledge/source-rebuild/README.md
-> knowledge/source-rebuild/local-customization-index.md
```

For repair tasks such as TUN failures, autostart not working, global-search errors, desktop AI residues, or damaged services, use `$HOME/.os-fix-skill/SKILL.md`.

## Coverage

- Tool global rules, Codex user-level configuration, full-access permission boundaries, and multi-tool loading rules.
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

Space cleanup, Kaiming/KARE layer control, ostree usage auditing, and desktop automation are better handled by companion applications. If a local development workspace exists, start from the workspace rules:

```text
$HOME/desktop-develop/AGENTS.md
```

This repository records enhancement strategy, safety boundaries, and reusable knowledge. Concrete UI, build, verification, dependency, and implementation rules belong in independent projects. Tool projects must still follow the system safety boundary: do not automatically delete ostree deployments, EFI files, GRUB config, loader entries, `/etc/fstab`, or partition tables.

On this machine, the usual development workspace entry is:

```text
$HOME/desktop-develop/AGENTS.md
```

That file only routes requests to projects; each concrete project continues from its own `AGENTS.md`.

## License

MIT License. See [LICENSE](LICENSE).
