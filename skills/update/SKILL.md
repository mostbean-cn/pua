---
name: update
description: "PUA 更新命令。识别源码安装或 marketplace 安装；能自动更新就自动更新，并覆盖更新 ~/.claude/commands/pua.md 裸 /pua alias。触发命令：/pua:update。"
license: MIT
---

# PUA Update

这是插件更新命令，对应 `/pua:update`。

## 目标

优先自动完成能自动完成的更新；如果当前安装方式不适合自动更新，就给出准确的下一步命令。无论哪种安装方式，都顺手补齐裸 `/pua` alias。

## 执行步骤

1. 先检查 `~/.claude/commands` 目录是否存在；如果不存在，先创建。
2. 无论 `~/.claude/commands/pua.md` 是否已存在，都覆盖写入该文件，内容如下：

```md
---
description: "PUA 裸命令别名。/pua [design|l1|l2|l3|update|version|任务描述]。默认等价于 /pua:auto。触发命令：/pua。"
argument-hint: "[design|l1|l2|l3|update|version]"
---

根据参数执行不同操作：

## 参数路由

- **无参数** 或任意任务描述 → 等价于执行 `/pua:auto`
- **design** → 等价于执行 `/pua:design`
- **l1** → 等价于执行 `/pua:l1`
- **l2** → 等价于执行 `/pua:l2`
- **l3** → 等价于执行 `/pua:l3`
- **update** → 等价于执行 `/pua:update`
- **version** → 等价于执行 `/pua:version`

## 执行规则

1. 先识别参数属于哪个路由
2. 用 Skill tool 加载对应 skill：
   - 默认路由加载 `pua:auto`
   - `design` 加载 `pua:design`
   - `l1` 加载 `pua:l1`
   - `l2` 加载 `pua:l2`
   - `l3` 加载 `pua:l3`
   - `update` 加载 `pua:update`
   - `version` 加载 `pua:version`
3. 如果有 `$ARGUMENTS` 里除了路由关键词之外的内容，作为任务描述传给对应 skill
```

3. 再检查 `~/.claude/plugins/pua` 是否存在。
5. 如果 `~/.claude/plugins/pua/.git` 存在，按源码安装处理：
   - 用 Bash 执行 `git -C "$HOME/.claude/plugins/pua" pull`
   - 如有需要，读取 `~/.claude/plugins/pua/pua/plugin.json` 查看版本
   - 明确告诉用户：更新后建议重启 Claude Code 使插件重新加载
6. 如果插件目录存在但没有 `.git`，按 marketplace 安装处理：
   - 不要编造别的更新方式
   - 直接告诉用户在当前会话执行：
     - `! claude plugin marketplace update`
     - `! claude plugin update pua@pua-skills`
   - 明确告诉用户：更新后建议重启 Claude Code
7. 如果既找不到源码目录，也无法确认安装方式：
   - 直接给出同样的 marketplace 更新命令
   - 说明这是最稳妥的标准更新路径

## 输出要求

- 先说明 alias 是新建了还是已存在
- 再说明检测到的安装方式
- 如果已自动执行更新，要说明是否成功
- 如果不能自动执行，要给出可直接复制的命令
- 不写空话，不长篇解释
