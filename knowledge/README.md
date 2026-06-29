# Knowledge 说明

`knowledge/` 保存可复用的具体增强章节。入口从 `references/<scenario>.md` 进入，不要一次性预加载整个目录。

渐进式披露链路：

```text
SKILL.md
-> references/<scenario>.md
-> knowledge/<scenario>/README.md
-> knowledge/<scenario>/<topic>.md
```

每次只读取最小必要链路。如果本索引和场景索引没有命中具体章节，停止继续加载 knowledge。不要通过 `find`、`rg` 或目录遍历把全库经验读入上下文；先基于当前需求设计方案，确认产生可复用经验后再新增最小章节。

每个具体章节建议包含：

- 背景和适用条件
- 前置检查
- 增强步骤
- 风险边界
- 验证步骤
- 回滚方式
- 需要沉淀的文件、patch 或配置路径
