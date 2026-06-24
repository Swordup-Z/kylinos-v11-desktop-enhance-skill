# kylinos-v11-desktop-enhance-skill

[English](README.en.md)

这是一个面向 KylinOS Desktop V11 的系统功能增强经验库，用来沉淀桌面系统本地客制化、默认行为调整、AI 工具配置和可回退增强流程。

它不是可执行程序，也不绑定某个 AI 工具的内置 skill 目录，而是一组给人和多个 AI 工具共同使用的结构化知识：人按目录查找经验，AI 工具从 `$HOME/.os-enhance-skill/SKILL.md` 开始按需渐进式读取。

## 适用范围

本仓库适用于系统原本能工作，但需要新增能力、改变默认行为或做本地客制化的场景，例如：

- UKUI 全局搜索、搜索引擎、自定义命令、托盘、快捷键、面板等增强。
- 应用安装体验、桌面入口、用户级安装方式增强。
- 网络策略、代理集成行为和 TUN 使用体验增强。
- DATA 工作区、分区使用、本地开发空间和清理策略。
- AI 工具全局提示词、权限、自动加载 skill 和桌面操作能力增强。
- 源码级功能增强、本地 patch 保存、构建和回滚策略。

如果系统已有行为异常、失效、报错、不能持久化或安装失败，应优先使用 `$HOME/.os-fix-skill/SKILL.md`。

## 安装

```bash
cd "$HOME"
git clone https://github.com/Swordup-Z/kylinos-v11-desktop-enhance-skill.git "$HOME/.os-enhance-skill"
```

入口文件：

```text
$HOME/.os-enhance-skill/SKILL.md
```

建议同时安装修复经验库，便于全局提示词按任务类型分流：

```bash
git clone https://github.com/Swordup-Z/kylinos-v11-desktop-fix-skill.git "$HOME/.os-fix-skill"
```

## 建议的全局提示词

把下面规则加入常用 AI 工具的用户级提示词，例如 Codex 的 `$HOME/.codex/AGENTS.md`、Claude Code 的 `$HOME/.claude/CLAUDE.md` 或 opencode 的 `$HOME/.config/opencode/AGENTS.md`：

```text
当用户处理 KylinOS Desktop V11 系统功能增强、本地客制化、默认行为调整、AI 工具配置、UKUI 行为扩展、应用安装体验、网络策略、存储策略、硬件能力增强或源码级功能增强时，先读取 $HOME/.os-enhance-skill/SKILL.md，再按其中 references 路由继续读取。

如果用户描述的是系统已有行为异常、失效、报错、不能持久化、安装失败或系统服务损坏，优先读取 $HOME/.os-fix-skill/SKILL.md。
```

## 目录结构

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

`references/` 是场景入口和策略路由层。`knowledge/feature-enhancement/<scenario>/README.md` 是场景内索引，具体 `<topic>.md` 保存背景、前置检查、增强步骤、验证、回滚和风险边界。源码级增强 patch 保存在对应场景的 `patches/<feature-id>/` 下，并通过 `PATCHSET.md` 记录基线、适用版本和迁移策略。

## License

MIT
