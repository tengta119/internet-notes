---
name: ai-project-docs
description: 为已存在的真实项目生成和维护 AI 辅助开发文档体系。分析当前项目代码，生成 docs/architecture.md（系统架构）、docs/business.md（业务逻辑）、docs/database.md（数据模型）、docs/development.md（开发流程），以及 docs/tasks/TODO/TASK-xxx.md 任务文档供 AI Coding Agent 执行。当用户要求初始化项目文档、生成/更新架构或业务文档、或将功能需求拆解为 Task 文档时使用此 skill。
---

# AI 项目文档体系

为已开发到一部分的真实项目，生成一套服务于后续 AI Agent 的文档体系。

## 文档体系结构

```
AGENTS.md → AI 必须遵守的规则
docs/
├── architecture.md → 系统现在是什么结构
├── business.md     → 业务现在怎么运行
├── database.md     → 数据现在怎么组织
├── development.md  → 项目现在怎么开发
│
├── decisions/
│   └── ADR-001-xxx.md → 为什么决定这么做
│
└── tasks/
    ├── TODO/
    │   └── TASK-001-xxx.md → 这次具体要做什么
    ├── DOING/
    └── DONE/
```

## 使用方式

根据用户需求，选择对应工作流。**执行任何工作流之前，必须先完整阅读对应的参考文档**，那里包含完整的分析范围、文档结构和输出要求：

| 任务 | 参考文档 | 产出 |
|---|---|---|
| 生成架构文档 | [references/architecture.md](references/architecture.md) | `docs/architecture.md` |
| 生成业务文档 | [references/business.md](references/business.md) | `docs/business.md` |
| 生成数据库文档 | [references/database.md](references/database.md) | `docs/database.md` |
| 生成开发文档 | [references/development.md](references/development.md) | `docs/development.md` |
| 拆解功能需求为 Task | [references/task.md](references/task.md) | `docs/tasks/TODO/TASK-xxx-<功能名称>.md` |

典型流程：

1. **文档初始化**（新项目首次接入）：依次执行 architecture → business → database → development 四个工作流。
2. **任务开发**：先阅读 `AGENTS.md` + `docs/` 下已有文档理解项目，再用 task 工作流将用户的功能需求拆解为 Task 文档，之后按 Task 实施。
3. **文档维护**：任务完成后检查 architecture.md / business.md / database.md 是否需要更新、是否需要新增 ADR。只有在项目事实发生变化时才修改文档，不要为了增加文档内容而修改文档。

## 通用铁律（所有工作流必须遵守）

这些规则适用于每一个工作流，参考文档中的具体要求是其细化：

1. **以现有代码为唯一事实依据。** 不要按常见项目模板、经验或 README 的表面描述猜测。无法确认的信息明确标记为"未知"或"待确认"，绝不编造。
2. **只分析和写文档，不改业务代码。** 不重构、不执行数据库结构变更、不为了让架构"看起来更合理"而修改现有设计、不提交 Git commit。每个工作流只允许创建/修改它自己的目标文档。
3. **严格区分三个层次：** 当前真实存在的、当前存在的问题（风险）、后续建议。绝不把建议写成现状，绝不把未来计划写成已实现功能。
4. **文档服务于后续 AI Agent。** 目标是让新的 AI 第一次进入项目时，不需要重新猜测，就能理解系统并安全地修改代码。每个文档末尾都有"AI 开发注意事项"章节。
5. **不泄露敏感信息。** 密码、Token、API Key、私钥等绝不写入文档，用 `<your-password>` 之类的占位符或"通过环境变量提供"代替。
6. **汇报要求。** 完成后必须汇报：读取了哪些关键文件、创建了哪个文档、是否修改了其他文件、哪些结论是代码明确证明的、哪些信息仍待确认。

## 生成 Task 文档时

用户的功能需求就是 task.md 参考文档中的【功能需求】占位符内容，替换后按文档执行。生成前必须先阅读 `AGENTS.md`、`docs/architecture.md`、`docs/business.md`（以及相关的 ADR、历史 Task、源码）。最终目标不是文档"写得详细"，而是让后续 Coding Agent **不需要重新猜测需求，就可以根据这份 Task 安全地完成实现**。
