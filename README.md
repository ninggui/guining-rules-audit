# 规则审计

![GitHub stars](https://img.shields.io/github/stars/ninggui/guining-rules-audit)
![License](https://img.shields.io/github/license/ninggui/guining-rules-audit)
[![SkillHub](https://img.shields.io/badge/SkillHub-在线安装-blue)](https://skillhub.cn/skills/guining-rules-audit)

检查用户近 7 天定的规则是否已固化到 memory/skill，缺失自动补。

## 这是什么

一个可复用的 AI Agent 技能（Skill），来自真实业务场景沉淀，含完整执行流程、避坑清单与验证步骤。

## 快速使用

将本仓库放入 Agent 技能目录后，用对应触发词调用（见 SKILL.md），Agent 会自动加载并执行完整流程。

## 核心能力

| 能力 | 说明 |
|------|------|
| 会话规则自动扫描 |
| 缺失规则自动补写 |
| 每周定时审计（周一） |

## 使用方式（安装）

- **Hermes**: 放入 `skills/` 目录
- **Claude**: 放入 `~/.claude/skills/`
- **其他 Agent**: 按对应 SKILL.md 格式放入技能目录
- **SkillHub 一键安装**: https://skillhub.cn/skills/guining-rules-audit

## 优势

- 防规则衰减（"你又忘了"）
- 自动化固化用户偏好
- 容量管理（优先保留高频/隐私类）

## 内容结构

- `SKILL.md` — 核心技能定义（触发条件、执行流程、避坑清单）
- `references/` — 可选参考文件

## 许可

MIT
