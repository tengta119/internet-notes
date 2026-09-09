
```
AGENTS.md → AI 必须遵守的规则
docs/
├── architecture.md → 系统现在是什么结构
├── business.md → 业务现在怎么运行
├── database.md → 数据现在怎么组织
├── development.md → 项目现在怎么开发
│
├── decisions/ 
│   ├── ADR-001-xxx.md → 为什么决定这么做
│   ├── ADR-002-xxx.md
│   └── ...
│
└── tasks/
    ├── TODO/
    │   ├── TASK-001-xxx.md → 这次具体要做什么
    │   └── TASK-002-xxx.md
    │
    ├── DOING/
    │   └── TASK-003-xxx.md
    │
    └── DONE/
        └── TASK-000-xxx.md
```

# Agent.md

```
## Documentation Rules

完成任务后，必须检查：

1. architecture.md 是否需要更新
2. business.md 是否需要更新
3. 是否需要新增 ADR （docs/decisions/ADR-001-xxx.md → 为什么决定这么做）

只有在项目事实发生变化时才修改文档。

不要为了增加文档内容而修改文档。
```