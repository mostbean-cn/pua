# pua

这是一个极简版 Claude Code 插件，提供 6 个入口：

- `/pua:auto`：默认自适应强度
- `/pua:l1`：最小执行纪律
- `/pua:l2`：系统排查
- `/pua:l3`：攻坚与结构化失败报告
- `/pua:update`：检测安装来源并执行/引导更新
- `/pua:version`：显示当前插件版本与更新提示

## 设计目标

`pua` 提炼的是外层 `pua` 的执行纪律精髓：更主动、少放弃、先验证再宣称完成。

它**不**引入复杂 flavor、hooks、telemetry、角色层级，也不做长篇表演式话术，只保留最基础、最直接的任务推进能力。

## 模式说明

### `/pua:auto`
默认模式。会先按 L1 执行；如果出现连续失败、缺少验证、原地打转或过早放弃，则自动升到 L2 / L3。

### `/pua:l1`
最小执行纪律层。适合普通开发任务，要求先查、先做、先验证，并顺手看一眼直接相关影响。

### `/pua:l2`
系统排查层。适合较难的调试任务，要求读报错、读上下文、搜索资料、列假设、做排除，并在失败后换本质不同的方案。

### `/pua:l3`
攻坚层。适合顽固问题和反复失败，强调系统化检查；如果仍未解决，也要输出结构化失败报告，而不是直接说做不了。

## 核心原则

- 闭环优先：完成前要有验证依据
- 事实优先：归因前先验证
- 先穷尽再放弃：动作没做完，不急着认输
- Owner 意识：能顺手处理的直接相关问题主动看一眼
- Iceberg 意识：修一个点时，顺手检查同类问题

## 安装

```bash
claude plugin marketplace add mostbean-cn/pua
claude plugin install pua@pua-skills
```

## 更新

- `/pua:update`：源码安装会尝试 `git pull`，marketplace 安装会提示执行标准更新命令。
- `/pua:version`：显示当前插件版本、插件名和更新提示。

```bash
claude plugin marketplace update
claude plugin update pua@pua-skills
```
