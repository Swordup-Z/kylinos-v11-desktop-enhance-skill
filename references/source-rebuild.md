# 系统功能增强：源码重编译

## 适用场景

- 系统设置界面或后端逻辑写死，需要源码级新增功能。
- 需要保存本地源码 commit、patch、构建清理策略和后续升级迁移路径。
- 例如 UKUI 全局搜索添加搜索引擎、自定义命令 provider 或设置页配置入口。

## 知识入口

进入源码重编译索引后，按“通用源码流程”“本地客制化索引”“patch 库”“组件级增强实现”选择一个具体知识；没有命中时停止，不要同时读取所有源码增强章节。

- [`../knowledge/source-rebuild/README.md`](../knowledge/source-rebuild/README.md)

| 子场景 | 快速判断 | 对应 knowledge |
| --- | --- | --- |
| 源码增强通用流程 | 需要判断是否必须源码级增强、维护模式、构建和安装安全边界 | `knowledge/source-rebuild/README.md` |
| 本地客制化索引 | 需要 DATA 工作区、`CUSTOMIZATION.md`、本地 commit、patch、回滚和状态记录 | `knowledge/source-rebuild/local-customization-index.md` |
| 可复用 patch 库 | 需要保存跨机器复用 patch、PATCHSET 元数据、基线节点和迁移规则 | `knowledge/source-rebuild/patch-library.md` |
| UKUI 具体源码增强 | 全局搜索、托盘角标等具体 UKUI 功能增强 | `knowledge/ukui/README.md` |

## 最小诊断

```bash
dpkg-query -W -f='${binary:Package} ${Version} ${Source}\n' <package>
apt-cache policy <package>
test -d /data/usershare/kylinos-local-sources && find /data/usershare/kylinos-local-sources -maxdepth 2 -name CUSTOMIZATION.md -print
```
