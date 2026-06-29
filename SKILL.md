---
name: kylinos-v11-desktop-enhance-skill
description: 处理 KylinOS Desktop V11 桌面系统功能增强、本地客制化、默认行为调整、AI 工具配置、UKUI 行为扩展、应用安装体验、网络策略、存储策略、硬件能力增强和源码级功能增强。适用于系统原本能工作但需要新增能力、改变默认行为或沉淀可复用增强流程的场景；系统已有行为异常、失效或报错时应优先使用 os-fix-skill。
---

# KylinOS Desktop V11 Enhance

这是 KylinOS Desktop V11 桌面系统功能增强经验库。入口文件位于 `$HOME/.os-enhance-skill/SKILL.md`，用于把可复用的本地增强流程沉淀为 AI 工具可按需读取的结构化知识。

## 使用边界

- 本 skill 只处理“系统原本能工作，但需要新增能力、改变默认行为或本地客制化”的任务。
- 如果用户描述的是已有能力异常、失效、报错、不能持久化、安装失败或系统服务损坏，先切换到 `$HOME/.os-fix-skill/SKILL.md`。
- 普通代码开发、文档编辑、Git 操作或与 KylinOS Desktop V11 桌面系统无关的问题不应加载本 skill。
- 不要把项目实现代码、一次性日志、用户专属路径或临时构建产物写入本仓库。

## 工作原则

- 先诊断需求和影响面，再设计增强方案，最后验证结果。
- 优先使用用户级配置、可回退配置和最小权限路径；只有确有必要时才修改系统路径。
- 涉及 `/usr`、`/etc`、`/opt`、systemd、系统包、设备节点、KSaf 策略、分区或系统级服务时，先运行 `mm-cli -s` 检查维护模式。只有确认当前是 maintain mode，才允许实际写入系统路径或修改系统服务。
- 如果当前不是维护模式，不要继续系统级增强。应让用户执行 `sudo mm-cli -o`，或在用户授权后执行 `pkexec mm-cli -o`，随后提醒用户重启系统后再继续。
- 所有增强方案都要说明前置检查、影响范围、回滚方式和验证步骤。
- 不要删除、移动或覆盖用户已有可执行文件、配置文件、订阅文件、代理核心、systemd 单元或用户数据，除非用户明确要求且已验证影响。
- 完成新的可复用增强后，按角色分流沉淀经验：普通使用者或无仓库写权限环境只生成 `$HOME/.os-enhance-skill-patches/` 下的本地 patch，保持 skill 仓库干净以便拉取上游；开发者维护仓库时才直接更新对应 `references/` 路由和 `knowledge/` 章节，并按当前开发环境规则处理后续仓库维护。

## 参考文档路由

先判断增强场景，再只读取最小匹配 reference。不要为了“保险”同时读取多个 reference；如果没有命中专门场景，只有明确属于维护流程、持久化策略或本地客制化通用规则时才读取 [references/system.md](references/system.md)，否则停止继续加载本 skill，先基于当前需求澄清或系统证据设计方案。

固定加载链路：

```text
SKILL.md
-> references/<scenario>.md
-> knowledge/<scenario>/README.md
-> knowledge/<scenario>/<topic>.md
```

只读取与当前增强需求匹配的一个具体 knowledge 章节。没有命中具体经验时，不要遍历整个 skill、不要预加载所有 reference 或 knowledge。

如果本地 skill 没有覆盖当前增强目标，先在工作树干净时尝试 `git fetch` 和 `git pull --ff-only` 同步上游；若存在本地改动，先保存为 `$HOME/.os-enhance-skill-patches/` 下的 patch 并跳过同步，不要强制覆盖或清理。同步失败不是阻塞条件，继续基于当前证据和通用能力设计方案。

- 系统维护流程、持久化策略、本地客制化规则增强：读取 [references/system.md](references/system.md)。
- 应用安装体验、桌面入口、用户级安装方式增强：读取 [references/applications.md](references/applications.md)。
- UKUI 全局搜索、搜索引擎、自定义命令、托盘、快捷键、面板等增强：读取 [references/ukui.md](references/ukui.md)。
- 网络策略、代理集成行为、TUN 使用体验增强：读取 [references/network.md](references/network.md)。
- 硬件能力恢复后的可选增强和稳定性策略：读取 [references/hardware.md](references/hardware.md)。
- DATA 工作区、分区使用、本地开发空间和清理策略：读取 [references/storage.md](references/storage.md)。
- AI 工具全局提示词、权限、自动加载 skill、桌面操作能力增强：读取 [references/agent-tools.md](references/agent-tools.md)。
- 源码级功能增强、本地 patch 保存、构建和清理策略：读取 [references/source-rebuild.md](references/source-rebuild.md)。

## 通用增强流程

1. 明确目标：新增能力、改变默认行为、改善体验，还是沉淀工具链规则。
2. 确认现状：读取配置、服务状态、实际路径、版本、日志和用户级设置来源。
3. 选择路径：优先用户级配置，其次应用级配置，再考虑系统级配置或源码 patch。
4. 设计回滚：保留原文件、记录修改点、准备撤销命令或 patch revert。
5. 执行修改：按维护模式和权限边界执行。
6. 验证效果：验证当前会话、重启后持久化、异常路径和回滚可用性。
7. 沉淀经验：新增或更新对应 `knowledge/<scenario>/` 章节。
