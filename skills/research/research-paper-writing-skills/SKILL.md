---
name: research-paper-writing-skills
description: "论文写作全流程：从引言到结论，每一步都有结构化模板。支持论文框架构建、各段生成、学术语言润色。"
version: "1.0.0"
user-invocable: true
argument-hint: "[论文写作 | 论文框架 | 论文润色 | 引言 | 方法 | 结果 | 讨论 | 结论 | abstract]"
---

# Research-Paper-Writing-Skills

## 概述

基于 Master-cai/Research-Paper-Writing-Skills（⭐4,999），提供论文写作全流程的结构化模板。

## 能力矩阵

| 章节 | 模板/提示词 | 说明 |
|------|------------|------|
| Introduction | 背景→gap→解决方案 | 引言构建 |
| Literature Review | 文献梳理→研究空白→分析定位 | 综述框架 |
| Methods | 设计→样本→设备→统计 | 方法描述 |
| Results | 主结果→图表→关键数值 | 结果展示 |
| Discussion | 主要发现→对比→解释→局限性 | 讨论框架 |
| Conclusion | 总结→意义→展望 | 结论生成 |
| Abstract | 一句话→背景→方法→结果→结论 | 摘要生成 |
| Title | 关键词→亮点→规范格式 | 标题优化 |
| Cover Letter | 新意→重要性→投稿声明 | 投稿信 |

## Agent 工作流

1. 用户指定论文章节或类型
2. AI 加载对应模板
3. 用户输入原始素材/数据
4. AI 按模板结构化输出
5. 用户审阅修改
6. 输出最终文本

## 与 PaperSpine 的关系

PaperSpine 侧重**全流程编排**（12 阶段从 intake→研究→写作→审核→提交），本 Skill 侧重**各章节的结构化模板**。两者互补：
- PaperSpine → 管理流程
- Research-Paper-Writing-Skills → 填充内容

## 触发方式

- `/论文写作 [章节]`
- `/论文框架`
- `/论文润色`
- `/abstract`
- `/cover-letter`
