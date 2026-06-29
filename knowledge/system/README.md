# 系统功能增强：系统基础

当前系统基础增强主要复用源码重编译和本地客制化索引规则：

- [`../source-rebuild/README.md`](../source-rebuild/README.md)
- [`../source-rebuild/local-customization-index.md`](../source-rebuild/local-customization-index.md)
- [local-experience-patches.md](local-experience-patches.md)：普通使用者无仓库写权限时，把本地增强经验保存为 sidecar patch，并保持 skill 仓库可同步上游。

只读取与当前问题匹配的一个章节：源码重编译通用流程读 `README.md`；本地源码、patch、回滚和索引策略读 `local-customization-index.md`；普通使用者本地经验沉淀读 `local-experience-patches.md`。没有命中时停止，不要继续遍历系统基础目录。
