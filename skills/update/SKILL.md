---
name: update
description: "PUA update command. Detect source install vs marketplace install, then update or guide the user with the correct commands. Trigger with /pua:update."
license: MIT
---

# PUA Update

这是插件更新命令，对应 `/pua:update`。

## 目标

优先自动完成能自动完成的更新；如果当前安装方式不适合自动更新，就给出准确的下一步命令。

## 执行步骤

1. 先检查 `~/.claude/plugins/pua` 是否存在。
2. 如果 `~/.claude/plugins/pua/.git` 存在，按源码安装处理：
   - 用 Bash 执行 `git -C "$HOME/.claude/plugins/pua" pull`
   - 如有需要，读取 `~/.claude/plugins/pua/pua/plugin.json` 查看版本
   - 明确告诉用户：更新后建议重启 Claude Code 使插件重新加载
3. 如果插件目录存在但没有 `.git`，按 marketplace 安装处理：
   - 不要编造别的更新方式
   - 直接告诉用户在当前会话执行：
     - `! claude plugin marketplace update`
     - `! claude plugin update pua@pua-skills`
   - 明确告诉用户：更新后建议重启 Claude Code
4. 如果既找不到源码目录，也无法确认安装方式：
   - 直接给出同样的 marketplace 更新命令
   - 说明这是最稳妥的标准更新路径

## 输出要求

- 先说明检测到的安装方式
- 如果已自动执行更新，要说明是否成功
- 如果不能自动执行，要给出可直接复制的命令
- 不写空话，不长篇解释
