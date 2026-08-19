---
name: user-rules-audit
slug: guining-rules-audit
displayName: guining-rules-audit
version: 1.0.0
description: 规则审计：检查用户近7天定的规则是否已固化到 memory/skill，缺失自动补。触发：用户说"你又忘了"或夜间迭代。
---
# 用户规则审计（guining-rules-audit）

## 背景

2026-08-18 用户观察：规则 1-2 天执行好、3-4 天衰减、一周忘。根因：memory 容量有限（~2200字符）+ 对话规则不落文件 + 无定期审计。

## 触发条件

- cron 每天 02:30 自动执行（guining-rules-audit）
- 用户说"你又忘了""规则没执行""这个规则不是说过吗"
- 夜间自主学习/迭代中做机制自检时

## 执行步骤

1. **采集**：session_search 搜索近7天对话，关键词：
   - "以后""记住""规则""要求""必须""不要""禁止""改成""统一""每次""一律"
   - 提取用户设定的规则/偏好/限制（排除一次性任务指令）
2. **对照**：读取 MEMORY.md / USER.md（memory tool）+ skills_list 全量
   - 每条规则检查是否在 memory 有"一句话触发条件"
   - 复杂规则检查是否有对应 skill 文件
3. **补缺**：
   - 缺失 → 写入 memory（一句话，精简）或 skill（详细流程）
   - memory 满 → 先压缩/合并旧条目再写（用 operations 批量）
4. **报告**：输出审计结果：
   - 新检出规则 N 条
   - 已补齐 M 条
   - 已在册无需处理 K 条
   - 写审计日志到 /home/user/learnings/daily-reports/ 当日文件
5. **验证**：对补齐的关键规则，下一轮对话中主动提及一次以确认生效

## 边界

- 只补"规则/偏好/限制"类，不补一次性任务进度
- 不确定是否算规则 → 先写入 memory（宁多勿漏，容量允许时）
- memory 容量紧张时：优先保留 高频触发/隐私红线/沟通偏好，任务进度类移出
- 禁止在审计中修改 cron 配置（那是运维范畴，另走队列）

## 关键文件

- memory: MEMORY.md / USER.md（memory tool 管理）
- 队列: /home/user/queue/pending_tasks.md
- 审计日志: /home/user/learnings/daily-reports/
