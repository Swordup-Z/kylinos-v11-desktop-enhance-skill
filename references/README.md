# References 路由说明

`references/` 是增强任务的策略路由入口，不保存详细实现过程。

## 场景入口

- [system.md](system.md)：维护流程、持久化策略、本地客制化通用规则。
- [applications.md](applications.md)：应用安装体验、桌面入口和用户级安装方式增强。
- [ukui.md](ukui.md)：UKUI 全局搜索、搜索引擎、自定义命令、托盘、截图默认行为等增强。
- [network.md](network.md)：网络策略和代理集成行为增强。
- [hardware.md](hardware.md)：硬件能力恢复后的可选增强记录。
- [storage.md](storage.md)：DATA 工作区、本地源码、构建、patch 和 KARE/Kaiming 空间治理策略。
- [agent-tools.md](agent-tools.md)：AI 工具全局提示词、权限、自动加载 skill。
- [source-rebuild.md](source-rebuild.md)：源码级功能增强、本地 patch 保存、构建和清理策略。

## 使用方式

1. 判断是否属于功能增强：系统原本能工作，但需要新增能力、改变默认行为或本地客制化。
2. 判断场景：system、applications、ukui、network、hardware、storage、agent-tools 或 source-rebuild。
3. 只读取一个最小匹配 reference。
4. reference 可以列出子场景和对应 knowledge 路径，但不直接展开具体增强过程。
5. 进入 `knowledge/<scenario>/README.md` 后，只读取与用户问题匹配的具体章节。
6. 如果 reference 和 knowledge 索引都没有命中具体章节，停止继续加载本 skill。基于当前需求、系统证据和通用能力设计方案，或先询问用户补充目标；不要遍历其他 reference 或整个 knowledge。

固定链路：

```text
SKILL.md
-> references/<scenario>.md
-> knowledge/<scenario>/README.md
-> knowledge/<scenario>/<topic>.md
```

只有问题明确属于维护流程、持久化策略或本地客制化通用规则时，才读取 [system.md](system.md)。如果只是“不知道该读哪个场景”，不要把 [system.md](system.md) 当成默认全文 fallback。
