# 本地增强经验 patch 队列

此文档用于普通使用者在没有本仓库写权限时沉淀本地增强经验。目标是让 `$HOME/.os-enhance-skill` 始终保持可 `git pull --ff-only` 的干净上游副本，同时不丢失本机新增经验。

## 适用场景

- 当前 enhance skill 尚未覆盖某个增强目标，但本次处理产生了可复用经验。
- 使用者没有仓库写权限，或不确定本地改动是否适合直接上游化。
- 本地已有修改会阻塞 `git pull --ff-only`，需要先把改动转为可管理 patch。

拥有仓库写权限的开发者维护本仓库时，先显式进入开发者维护模式。只有本地标记为维护者且 dry-run push 通过，才直接修改仓库文档、commit，并按当前开发环境的全局提示词或项目规则 push；否则仍走 sidecar patch，避免制造本地分叉。

维护者检查命令：

```bash
skill_dir="$HOME/.os-enhance-skill"; if git -C "$skill_dir" push --dry-run --porcelain origin HEAD:refs/heads/main >/dev/null 2>&1; then git -C "$skill_dir" config --local osSkill.maintainer true; else git -C "$skill_dir" config --local --unset osSkill.maintainer 2>/dev/null || true; fi
```

后续沉淀经验前再确认：

```bash
test "$(git -C "$HOME/.os-enhance-skill" config --get osSkill.maintainer)" = true && \
  git -C "$HOME/.os-enhance-skill" push --dry-run --porcelain origin HEAD:refs/heads/main >/dev/null
```

不要采用“无权限时先 commit、导出 patch、再 reset 到远端”的流程；不要自动切换开发分支保存普通使用者经验。这两种方式都会让普通使用者的 skill 仓库更容易偏离上游。

## 存放位置

普通使用者的本地增强经验保存到 sidecar 目录，不直接写入 skill 主工作树：

```text
$HOME/.os-enhance-skill-patches/INDEX.md
$HOME/.os-enhance-skill-patches/patches/<YYYYMMDD>-<scenario>-<topic>.patch
```

`INDEX.md` 至少记录：

- 场景分类，例如 `ukui`、`source-rebuild`、`agent-tools`。
- 增强目标摘要。
- patch 文件路径。
- 生成 patch 时的 skill commit。
- 验证状态：`draft`、`tested`、`needs-review` 或 `upstreamed`。
- 是否已经合入上游仓库。

## 生成 patch

使用临时 worktree 或临时副本生成 patch，避免污染主 skill 目录。推荐流程：

```bash
stamp="$(date +%Y%m%d-%H%M%S)"
worktree="/tmp/os-enhance-skill-patch-$stamp"
patch_dir="$HOME/.os-enhance-skill-patches/patches"
mkdir -p "$patch_dir"
git -C "$HOME/.os-enhance-skill" worktree add --detach "$worktree" HEAD
# 在 "$worktree" 中新增或修改 references/、knowledge/ 或必要的 SKILL.md 路由。
git -C "$worktree" add -N references knowledge SKILL.md 2>/dev/null || true
git -C "$worktree" diff --binary > "$patch_dir/${stamp}-<scenario>-<topic>.patch"
git -C "$HOME/.os-enhance-skill" worktree remove "$worktree"
```

如果主 skill 工作树已经有本地修改，先用 `git diff --binary` 导出到 patch，再向用户说明主工作树已不适合直接同步上游。不要自动执行 `git reset`、`git checkout --` 或删除文件。

## 使用 patch

处理后续同类增强任务时，只有场景匹配才读取 `$HOME/.os-enhance-skill-patches/INDEX.md` 中对应条目和单个 patch 文件。不要一次性加载整个 patch 目录。

默认只把 sidecar patch 当作本机参考材料读取；除非用户明确要求临时套用，不要把 patch 应用到 `$HOME/.os-enhance-skill` 主工作树。若 patch 已被开发者上游化，应把索引状态改为 `upstreamed`，后续优先使用上游 skill 内容。
