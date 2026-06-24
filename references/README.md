# References 路由说明

`references/` 是增强任务的策略路由入口，不保存详细实现过程。

## 使用方式

1. 判断是否属于功能增强：系统原本能工作，但需要新增能力、改变默认行为或本地客制化。
2. 判断场景：system、applications、ukui、network、hardware、storage、agent-tools 或 source-rebuild。
3. 只读取一个最小匹配 reference。
4. reference 只指向该场景的 knowledge 索引，不直接展开所有细分知识。
5. 进入 `knowledge/feature-enhancement/<scenario>/README.md` 后，只读取与用户问题匹配的具体章节。

固定链路：

```text
SKILL.md
-> references/feature-enhancement/<scenario>.md
-> knowledge/feature-enhancement/<scenario>/README.md
-> knowledge/feature-enhancement/<scenario>/<topic>.md
```

未命中细分场景时，读取 `references/feature-enhancement/system.md`。

