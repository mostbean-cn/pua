---
name: uninstall
description: "PUA 卸载命令。给出正确卸载步骤与卸载后的必要提醒。触发命令：/pua:uninstall。"
license: MIT
---

# PUA Uninstall

这是卸载命令，对应 `/pua:uninstall`。

## 目标

优先清楚告诉用户如何卸载，并补充卸载后的必要提醒。

## 执行步骤

1. 根据安装方式给出卸载命令。
2. 优先建议用户在当前会话执行 Claude Code 的标准卸载命令：`! claude plugin uninstall pua@pua-skills`。
3. 如果是源码安装目录，也可以提示用户手动删除 `~/.claude/plugins/pua`。
4. 明确告诉用户：卸载后建议重启 Claude Code。

## 建议输出

- 推荐执行：`! claude plugin uninstall pua@pua-skills`
- 如果是源码安装，可补充：手动删除 `~/.claude/plugins/pua`
- 最后提醒重启 Claude Code

## 输出要求

- 简洁中文
- 直接给步骤
- 不写长篇解释
