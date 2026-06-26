# KARE/Kaiming 空间清理策略增强

## 适用场景

- 为 KylinOS Desktop V11 的空间清理工具增加 KARE/Kaiming 针对性清理能力。
- 需要判断哪些 Kaiming 层、KARE 写入层或缓存状态可以安全移动到回滚隔离区。
- 需要解释“容器占用不断增长”是否能通过旧版本容器清理解决。

## 存储模型

Kaiming 常见路径：

- `/var/opt/kaiming/layers/stable/<arch>/<kind>/<ref>/<module>/<version>`：已安装应用、runtime、base 的版本层。
- `/var/opt/kaiming/info/*.list`：当前版本引用清单，可用于判断某个 stable layer 是否仍属于当前版本。
- `/var/opt/kaiming/repo`：对象仓库、索引和临时状态。不能仅凭目录大小自动删除。
- `/var/opt/kaiming/home`：应用状态或用户状态入口。不能作为自动清理候选。

KARE 常见路径：

- `/var/opt/kare-applications/base`：兼容环境基线，不作为清理候选。
- `/var/opt/kare-applications/<profile>/upper`：overlay 写入层，可能包含 cache、tmp、log，也可能包含真实状态。
- `/var/opt/kare-applications/<profile>/work`：overlay 工作目录，只有确认未挂载时才可考虑。
- `/var/opt/kare-applications/<profile>/merge`：挂载后的合并视图，不能直接清理。

`/opt/kare-applications` 可能和 `/var/opt/kare-applications` 指向同一套内容或被 overlay 参数引用。诊断和清理时应统一规范到 `/var/opt/kare-applications` 视角。

## 诊断步骤

```bash
mm-cli -s
findmnt -t overlay -o TARGET,SOURCE,OPTIONS | rg 'kare|kaiming|TARGET'
find /var/opt/kaiming/layers/stable -mindepth 5 -maxdepth 5 -type d -print
find /var/opt/kaiming/info -name '*.list' -type f -print
du -sh /var/opt/kaiming /var/opt/kaiming/layers /var/opt/kaiming/repo /var/opt/kaiming/home 2>/dev/null
du -sh /var/opt/kare-applications/*/upper /var/opt/kare-applications/*/work 2>/dev/null
```

## 候选判定

可作为自动候选：

- Kaiming stable layer 不在 `/var/opt/kaiming/info/*.list` 当前引用清单中。
- 该 Kaiming layer 未出现在任何 `/proc/<pid>/mountinfo` 中。
- KARE profile 的 `upper/work` 未出现在当前 overlay `upperdir/workdir` 中。
- 非活跃 KARE `upper` 下明确属于缓存、临时或日志的目录，例如 `upper/var/cache`、`upper/var/tmp`、`upper/tmp`、`upper/root/.cache`、`upper/var/log`。

只展示不自动清理：

- 当前仍被 Kaiming info 引用的 layer。
- 当前被进程挂载或使用的 Kaiming layer。
- 正在 overlay 挂载使用的 KARE `upper/work`。
- Kaiming repo 对象仓库、repo state、repo tmp/cache。
- Kaiming home 或应用运行状态目录。
- KARE base、merge 视图、真实应用数据目录。

## 执行策略

- 清理执行前必须重新扫描候选并按候选 ID 重新校验，不信任 GUI 传入的路径。
- 系统级移动必须要求 root 和 maintain mode。
- 不直接删除候选；移动到 DATA 回滚隔离区，例如：

```text
/data/usershare/kylinos-system-rollbacks/storage/kylin-space-guard-cleanup/<timestamp>/
```

- 执行后记录 JSON 结果：候选 ID、源路径、目标路径、释放字节、失败原因。
- 回滚方式是把隔离区中的路径按原相对路径移回原位置；回滚前同样需要确认目标路径不存在或已备份。

## 交互建议

- 页面名称使用“KARE/Kaiming 清理”或“运行环境清理”，不要只叫“旧版本容器清理”。
- 状态卡片至少展示：清理项总数、可清理容量、正在使用/仅统计项数量。
- 二级列表按候选逐项展示，禁用当前使用项，显示原因而不是只显示路径。
- “运行”按钮必须在至少选择一个可清理项后才启用。
- 详情弹窗应说明为什么可清理或为什么只统计，并展示原始路径和预计释放空间。

## 风险边界

- 如果用户描述的是“某个节点状态持续增长”，旧版本层清理通常不能解决；应先确认增长发生在 repo、home、KARE upper 还是应用自身数据目录。
- 对象仓库类数据需要官方 prune/gc 能力或引用图校验；没有官方工具或严格引用校验前，不要自动删除。
- 活跃 overlay 写入层的 cache/tmp 即使看似可清，也应默认只统计，避免破坏正在运行的兼容环境。
