---
name: version
description: "PUA 版本命令。读取本地插件元数据，显示版本号、包名与更新提示。触发命令：/pua:version。"
license: MIT
---

# PUA Version

这是版本查看命令，对应 `/pua:version`。

## 执行步骤

1. 优先读取当前插件目录下的 `plugin.json`。
2. 输出以下信息：
   - 插件名
   - 版本号
   - repository 或 homepage（如果存在）
3. 如果读取失败，明确说明没有找到本地元数据文件。
4. 结尾补一句更新提示：
   - 可使用 `/pua:update`
   - 或执行标准更新命令

## 输出要求

- 简洁中文
- 直接展示结果
- 不写长篇解释
