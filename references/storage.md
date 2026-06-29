# 系统功能增强：存储与工作区

## 适用场景

- 希望把本地源码、构建和 patch 工作区放到 DATA 分区。
- 需要制定分区、挂载或开发工作区的长期使用策略。

## 知识入口

进入存储与工作区索引后，按 DATA 工作区、源码目录、patch、回滚分类或 KARE/Kaiming 空间治理选择一个具体知识；没有命中时停止，不要继续遍历存储知识。

- [`../knowledge/storage/README.md`](../knowledge/storage/README.md)

| 子场景 | 快速判断 | 对应 knowledge |
| --- | --- | --- |
| 本地源码工作区 | 需要 DATA 分区源码、构建、patch、回滚目录策略 | `knowledge/source-rebuild/local-customization-index.md` |
| KARE/Kaiming 空间治理工具策略 | 需要设计清理候选判定、回滚隔离策略或独立工具安全边界 | `knowledge/storage/kare-kaiming-cleanup.md` |

## 最小诊断

```bash
findmnt -T /data/usershare
df -hT /data/usershare "$HOME"
```
