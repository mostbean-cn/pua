---
name: uninstall
description: "PUA uninstall command. Show the correct uninstall steps and optionally remove ~/.claude/commands/pua.md if it exists. Trigger with /pua:uninstall."
license: MIT
---

# PUA Uninstall

这是卸载命令，对应 `/pua:uninstall`。

## 目标

优先清楚告诉用户如何卸载；如果本地存在裸 `/pua` alias，就顺手一并移除。

## 执行步骤

1. 先检查 `~/.claude/commands/pua.md` 是否存在。
2. 如果 alias 存在：
   - 询问用户是否要一并删除 `~/.claude/commands/pua.md`。
   - 如果用户同意，再执行删除。
   - 如果用户不同意，就保留并说明。
3. 再根据安装方式给出卸载命令：
   - 优先建议用户在当前会话执行 Claude Code 的标准卸载命令。
   - 如果是源码安装目录，也可以提示用户手动删除 `~/.claude/plugins/pua`。
4. 明确告诉用户：卸载后建议重启 Claude Code。

## 建议输出

- 检测到 alias 是否存在
- 推荐执行：`! claude plugin uninstall pua@pua-skills`
- 如果是源码安装，可补充：手动删除 `~/.claude/plugins/pua`
- 最后提醒重启 Claude Code

## 输出要求

- 简洁中文
- 直接给步骤
- 不写长篇解释
