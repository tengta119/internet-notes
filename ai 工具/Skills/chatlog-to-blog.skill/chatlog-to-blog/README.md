# chatlog-to-blog

把 GPT / ChatGPT 聊天记录转换成技术博客。

## 适用场景

适合把平时和 ChatGPT 讨论 Java、Spring、Redis、RocketMQ、JVM、MySQL、Reactor、Agent 等技术问题的聊天记录，整理成长期可维护的博客文章。

## 基本用法

把聊天记录文件或目录提供给 Agent，然后让 Agent 调用本 Skill。

示例：

```text
使用 chatlog-to-blog Skill。
读取 ./chatlogs/ 中的聊天记录，
从中找出最适合写成技术博客的主题，
生成 article.md、analysis.md 和 metadata.md。
不要编造聊天记录中没有的项目事实。
```

## 推荐目录

```text
project/
├── chatlogs/
│   ├── chat-001.json
│   ├── chat-002.json
│   └── ...
└── output/
```

## 输出

```text
output/
├── article.md
├── analysis.md
└── metadata.md
```

## 核心思想

不是“聊天记录摘要器”，而是：

```text
聊天记录
   ↓
技术问题
   ↓
知识模型
   ↓
真实证据
   ↓
重新组织
   ↓
技术博客
```

Skill 特别强调区分：

- 用户真实提供的信息
- 聊天中验证过的结论
- AI 推测
- 后续泛化解释

这样可以降低把 AI 幻觉写进个人技术博客的风险。
