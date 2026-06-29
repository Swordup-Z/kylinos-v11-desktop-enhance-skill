# UKUI 截图默认保存目录

## 适用场景

- KylinOS Desktop V11 的 `kylin-screenshot` 能正常截图，但用户希望把默认保存位置从图片根目录改到独立子目录。
- 只调整当前用户的截图工具偏好，不修改系统包、desktop 文件或全局配置。

## 前置检查

```bash
command -v kylin-screenshot || true
gsettings list-recursively org.ukui.screenshot 2>/dev/null || true
```

重点确认 `org.ukui.screenshot screenshot-path` 是否存在。该键通常保存截图默认目录，值需要使用绝对路径并保留末尾 `/`。

## 增强步骤

优先使用 XDG 图片目录，避免硬编码语言环境下的目录名：

```bash
pictures_dir="$(xdg-user-dir PICTURES 2>/dev/null || printf '%s/图片\n' "$HOME")"
target_dir="$pictures_dir/截图"
mkdir -p "$target_dir"
gsettings set org.ukui.screenshot screenshot-path "$target_dir/"
```

如果目标目录使用英文名，可把 `target_dir` 改为 `"$pictures_dir/Screenshots"`。

## 验证

```bash
gsettings get org.ukui.screenshot screenshot-path
ls -ld "$target_dir"
kylin-screenshot full
find "$target_dir" -maxdepth 1 -type f -name '*.png' -printf '%TY-%Tm-%Td %TH:%TM:%TS %p\n'
```

验证重点：

- `screenshot-path` 返回目标目录，且末尾带 `/`。
- 目标目录存在并归当前用户所有。
- 实际截图文件落在目标目录。

## 回滚

恢复到图片目录根路径：

```bash
pictures_dir="$(xdg-user-dir PICTURES 2>/dev/null || printf '%s/图片\n' "$HOME")"
gsettings set org.ukui.screenshot screenshot-path "$pictures_dir/"
```

如果只想恢复 schema 默认值，可使用：

```bash
gsettings reset org.ukui.screenshot screenshot-path
```

## 风险边界

- 这是用户级 gsettings 配置，不需要维护模式，也不应修改 `/usr/share/applications/kylin-screenshot.desktop`。
- 不要删除原图片目录里的截图文件；目录迁移只影响后续截图保存位置。
- 如果命令行直接运行 `kylin-screenshot full` 没有生成文件，先确认当前图形会话是否允许截图，再检查 `$HOME/.log/kylin-screenshot.log`。
