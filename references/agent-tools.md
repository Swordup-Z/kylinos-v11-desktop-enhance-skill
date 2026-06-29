# 系统功能增强：AI 工具配置

## 适用场景

- Codex、Claude Code、opencode 等工具的全局提示词。
- 默认权限、full access、修复/增强 skill 自动加载和渐进式披露。
- 让 AI 工具在系统修复或功能增强完成后自动沉淀经验到对应仓库。

## 知识入口

AI 工具进入配置索引后，按 Codex 本地配置或多工具全局提示词选择具体知识；没有命中时停止，不要继续遍历工具配置知识。

- [`../knowledge/agent-tools/README.md`](../knowledge/agent-tools/README.md)

| 子场景 | 快速判断 | 对应 knowledge |
| --- | --- | --- |
| Codex 用户级配置 | 需要调整 Codex 配置、权限、full access 或本机 Codex 行为 | `knowledge/agent-tools/codex-config.md` |
| 多工具全局提示词 | 需要 Codex/Claude Code/opencode 自动加载 fix/enhance 经验库 | `knowledge/agent-tools/global-prompts.md` |

## 最小诊断

```bash
test -f "$HOME/.codex/config.toml" && sed -n '1,160p' "$HOME/.codex/config.toml"
test -f "$HOME/AGENTS.md" && sed -n '1,200p' "$HOME/AGENTS.md"
```
