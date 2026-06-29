# kylinos-v11-desktop-enhance-skill

[English](README.en.md)

这是一个面向 KylinOS Desktop V11 的系统功能增强经验库，用来沉淀桌面系统原本能工作、但需要新增能力、改变默认行为、本地客制化或源码级功能增强时的可复用流程。它不是可执行程序，也不绑定某个工具的内置目录；入口文件为 `$HOME/.os-enhance-skill/SKILL.md`，详细内容按 `references/` 和 `knowledge/` 渐进展开。

内容覆盖 UKUI 全局搜索、搜索引擎、自定义命令、托盘状态角标、工具全局规则、Codex 用户级配置、DATA 工作区、本地源码客制化、源码 patch 保存、构建与回滚策略等场景。

系统已有能力异常、失效、报错、不能持久化、安装失败或系统服务损坏的修复流程属于 `$HOME/.os-fix-skill`。

## 先安装一个 AI 编程工具

如果还没有可用的 AI 编程工具，先安装 Codex、Claude Code 或 opencode 之一。下面命令面向 KylinOS Desktop V11 这类 Linux 桌面终端；更多安装方式见对应官方文档。

### Codex

官方文档：

- Codex CLI：https://developers.openai.com/codex/cli
- Codex 快速开始：https://developers.openai.com/codex/quickstart

推荐安装命令：

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

安装后启动：

```bash
codex
```

### Claude Code

官方文档：

- Claude Code 快速开始：https://docs.anthropic.com/en/docs/claude-code/quickstart
- Claude Code 设置：https://docs.anthropic.com/en/docs/claude-code/setup

推荐安装命令：

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

安装后启动：

```bash
claude
```

### opencode

官方文档：

- opencode 文档：https://opencode.ai/docs/
- opencode 下载：https://opencode.ai/download

推荐安装命令：

```bash
curl -fsSL https://opencode.ai/install | bash
```

安装后启动：

```bash
opencode
```

如果系统策略不允许 `curl | sh` 或 `curl | bash`，打开上面的官方页面，按当前 Linux 桌面环境选择独立安装包、npm 或其他受信任的安装方式。

## 安装本经验库

```bash
cd "$HOME"
git clone https://github.com/Swordup-Z/kylinos-v11-desktop-enhance-skill.git "$HOME/.os-enhance-skill"
```

### 复制给 AI 工具执行安装

也可以把下面整段复制给 Codex、Claude Code 或 opencode，让 AI 工具代为安装并接入用户级规则文件：

```text
请帮我在本机安装 KylinOS Desktop V11 系统功能增强经验库 kylinos-v11-desktop-enhance-skill，并接入当前 AI 工具的用户级规则文件。

执行要求：
1. 先检查 git 是否可用。
2. 如果 $HOME/.os-enhance-skill 不存在，执行：
   git clone https://github.com/Swordup-Z/kylinos-v11-desktop-enhance-skill.git "$HOME/.os-enhance-skill"
3. 如果 $HOME/.os-enhance-skill 已存在且是 git 仓库，只允许执行非破坏更新：
   git -C "$HOME/.os-enhance-skill" status -sb
   git -C "$HOME/.os-enhance-skill" fetch --prune
   git -C "$HOME/.os-enhance-skill" pull --ff-only
   如果存在本地改动、分支分叉或 fast-forward 失败，不要覆盖，直接说明原因。
4. 如果 $HOME/.os-enhance-skill 已存在但不是 git 仓库，不要删除或覆盖，直接停止并说明原因。
5. 确认 $HOME/.os-enhance-skill/SKILL.md 存在。
6. 必要时创建当前 AI 工具用户级规则文件的父目录。
7. 将下面规则追加到当前 AI 工具的用户级规则文件；如果无法判断当前工具，则优先询问我。不要覆盖已有内容，已有同等规则时不要重复追加。

规则文件位置：
- Codex: $HOME/.codex/AGENTS.md
- Claude Code: $HOME/.claude/CLAUDE.md
- opencode: $HOME/.config/opencode/AGENTS.md

需要追加的规则：
当用户处理 KylinOS Desktop V11 系统功能增强、本地客制化、默认行为调整、AI 工具配置、UKUI 行为扩展、应用安装体验、网络策略、存储策略、硬件能力增强或源码级功能增强，且系统原本能工作但需要新增能力、改变默认行为或沉淀可复用增强流程时，默认使用 $HOME/.os-enhance-skill/SKILL.md 作为经验入口。开始处理系统功能增强前，先读取 $HOME/.os-enhance-skill/SKILL.md，再按其中“参考文档路由”选择性读取 references/<scenario>.md；随后只读取该 reference 指向的 knowledge/<scenario>/README.md，以及与当前目标匹配的一个具体 knowledge 章节。如果没有命中具体 reference 或 knowledge 章节，不要遍历整个 skill；只有目标明确属于维护流程、持久化策略或本地客制化通用规则时，才读取 $HOME/.os-enhance-skill/references/system.md。处理任务时遵循“先诊断需求和影响面、再设计增强方案、最后验证和记录回滚”；涉及 /usr、/etc、/opt、系统包、系统服务、设备节点、分区、KSaf 策略等系统级增强前，必须先运行 mm-cli -s 检查维护模式，只有确认当前是 maintain mode 才允许实际修改系统路径、系统服务或系统包。

完成后请告诉我仓库路径、已更新的规则文件路径，以及是否因为已有本地改动或分支状态跳过了更新。
```

入口文件是：

```text
$HOME/.os-enhance-skill/SKILL.md
```

常见工具的用户级规则文件位置：

```text
Codex:       $HOME/.codex/AGENTS.md
Claude Code: $HOME/.claude/CLAUDE.md
opencode:    $HOME/.config/opencode/AGENTS.md
```

把这些规则文件接入本经验库后，KylinOS Desktop V11 系统功能增强、本地客制化、默认行为调整、工具配置或源码级功能增强可从 `$HOME/.os-enhance-skill/SKILL.md` 进入，再按其中的 `references/` 路由继续查阅。系统修复问题由 `$HOME/.os-fix-skill` 维护。

系统增强使用固定会话名，例如 `os-enhance`。之后遇到系统增强任务时，恢复同一个会话继续处理：

```bash
codex resume os-enhance
claude resume os-enhance
opencode resume os-enhance
```

## 整体架构

本仓库面向系统功能增强场景：系统原本能工作，但用户需要新增能力、改变默认行为、本地客制化或沉淀可复用增强流程。例如给 UKUI 全局搜索增加 Bing/Google、自定义命令面板、托盘输入法状态角标、保存本地源码 patch、配置工具全局规则。

增强内容按场景分类：

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

## 目录结构

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

`references/` 是场景入口和策略路由层，包含适用场景、简短说明、知识入口和最小诊断。`knowledge/<scenario>/README.md` 是场景内索引，负责把增强需求继续路由到具体章节。具体 `<topic>.md` 保存背景、前置检查、增强步骤、验证、回滚和风险边界。通过源码修改实现的可复用增强还会在同场景 `patches/<feature-id>/` 下保存 patch 集和 `PATCHSET.md` 元数据。

固定加载链路：

```text
增强需求
-> 实际场景 reference
-> 场景 knowledge README
-> 具体细分 knowledge
```

## 路由示例

配置 Codex/Claude/opencode 自动加载共享经验库：

```text
SKILL.md
-> references/agent-tools.md
-> knowledge/agent-tools/README.md
-> knowledge/agent-tools/global-prompts.md
```

给 UKUI 全局搜索增加自定义命令面板：

```text
SKILL.md
-> references/ukui.md
-> knowledge/ukui/README.md
-> knowledge/ukui/search-command-provider.md
```

给 UKUI 全局搜索增加 Bing/Google 等搜索引擎：

```text
SKILL.md
-> references/ukui.md
-> knowledge/ukui/README.md
-> knowledge/ukui/search-web-engine.md
```

规划 DATA 分区本地源码客制化工作区：

```text
SKILL.md
-> references/source-rebuild.md
-> knowledge/source-rebuild/README.md
-> knowledge/source-rebuild/local-customization-index.md
```

如果任务是 TUN 失败、开机自启动不生效、全局搜索异常、AI 组件残留、系统服务损坏等修复类问题，请使用 `$HOME/.os-fix-skill/SKILL.md`。

## 当前覆盖范围

- 工具全局规则、Codex 用户级配置、full access 权限边界和多工具加载规则。
- UKUI 全局搜索搜索引擎增强。
- UKUI 全局搜索自定义命令 provider 和图形化命令配置。
- UKUI 托盘输入法状态角标等桌面交互增强。
- 本地源码客制化工作区、commit、patch、构建产物清理策略。
- 可复用源码 patch 集、上游仓库、基线节点和冲突迁移策略。
- DATA 分区用于本地源码、构建、回滚和开发工作的目录策略。
- 应用安装体验、桌面入口、用户级安装方式、网络策略、硬件能力增强等后续可扩展分类。

## 安全边界

KylinOS Desktop V11 上的系统级增强通常需要维护模式。涉及 `/usr`、`/etc`、`/opt`、系统包、systemd、设备节点、分区、KSaf 或系统服务时，应先确认维护模式：

```bash
mm-cli -s
```

进入维护模式：

```bash
sudo mm-cli -o
```

退出维护模式并保存：

```bash
sudo mm-cli -c -a
```

切换维护模式后通常需要重启。具体操作流程以 `SKILL.md` 和对应 reference/knowledge 章节为准。

增强方案应优先使用用户级配置、可回退配置和最小权限路径；确需系统级源码 patch 或替换系统文件时，必须记录前置检查、影响范围、回滚方式和验证步骤。

## 独立工具

空间清理、Kaiming/KARE 应用层治理、ostree 占用审计、桌面自动化操作等任务适合由独立应用承载。若本机存在独立开发工作区，可从工作区规则文件进入：

```text
$HOME/desktop-develop/AGENTS.md
```

本仓库记录增强策略、安全边界和可复用经验；具体 UI、构建、验证、依赖选择和项目实现规则应维护在独立项目内。工具类项目仍必须遵守系统安全边界：不得自动删除 ostree deployment、EFI、GRUB、loader entries、`/etc/fstab` 或分区表。

如果使用本机的开发工作区，入口通常是：

```text
$HOME/desktop-develop/AGENTS.md
```

该文件只做项目路由；具体项目继续读取各自目录下的 `AGENTS.md`。

## License

当前仓库使用 MIT License，见 [LICENSE](LICENSE)。
