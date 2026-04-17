---
name: better-skill-creator
description: "适用：创建、重构或评审本地 Skill 包；不适用：一次性 Prompt、低频文档整理或与 Skill 无关的代码任务；产出：按最佳实践设计的 skill 目录与 supporting files。"
metadata:
  author: "RookieZoe<i@rookiezoe.com>"
  version: "1.1.0"
  tags: [skills, skill-design]
  support: "https://github.com/RookieZoe/zoe-skills"
---

# 更好的 Skill 创建器

## 路由

- 适用：用户要新建 skill、升级现有 skill、给 skill 做 review/重构，或把零散 prompt、脚本、模板整理成 skill 包。
- 不适用：用户只要一句一次性 prompt、只想总结文档、只是在修普通代码 bug，或这个需求更适合写成文档而不是 skill。
- 产出：一个边界清晰、按需加载、结构完整的 skill 目录，至少包含 `SKILL.md`，必要时补 `references/`、`assets/`、`scripts/`。
- 反例："给我一句 system prompt"、"帮我总结这篇文章"、"修一下这个 Python 报错"

## 流程

第 1 步：先读取 `references/skill-triage.md`，判断这个需求是否真的应该做成 skill；如果不应该，明确给出更合适的替代方案。
第 2 步：读取 `references/pattern-selector.md`，先在五种设计模式里选一个主模式；只有在确有必要时才组合次级模式，并保持单一主模式对外路由。
第 3 步：读取 `references/routing-and-loading.md`，写出短而准的 `description`，以及 `SKILL.md` 中的“适用 / 不适用 / 产出 / 反例”。
第 4 步：读取 `references/yaml-head-rules.md`，先组装合法的 YAML 头部，确保 `name`、`description` 和可选字段都符合规范。
第 5 步：读取 `references/package-assembly.md`，决定哪些内容放进 `SKILL.md`，哪些拆到 `references/`、`assets/`、`scripts/`；如果用了组合模式，要把次级模式细节拆到对应步骤再按需加载。
第 6 步：直接创建或更新目标 skill 文件；如果关键上下文缺失，只问最少量、最必要的问题。
第 7 步：读取 `references/review-checklist.md`，对结果做一轮自检；如果发现它其实不该是 skill、模式选错了，或路由描述不清，就继续修正。

## 约束

- 先判断“应不应该做成 skill”，再判断“怎么做成 skill”。
- 一个 skill 只做一个主任务，并且只声明一个主设计模式。
- 设计模式可以组合，但组合只能服务于主任务；`metadata.pattern`、`description` 和对外路由仍然必须保持一个清晰主模式。
- YAML 头部必须合法：`name` 与目录名一致、只用小写字母/数字/连字符；`description` 用自然语言描述触发条件，且不要包含 XML 尖括号。
- 不要试图“蒸馏一个人”；要沉淀的是可复用的 SOP、约束、资源和输出规则。
- `description` 必须短、像路由条件，且包含“适用 / 不适用 / 产出”。
- `license`、`compatibility`、`allowed-tools`、`metadata` 只在确有价值时才填写；不要为了“看起来完整”而凑字段。
- `SKILL.md` 只保留路由、流程和约束；详细规则拆到 supporting files。
- 如果有次级模式，只在对应步骤引用它所需的 `references/` 或 `assets/`；不要把所有模式说明一次性塞进常驻上下文。
- 需要代码时，把代码放到 `scripts/`；不要把实现散落在 skill 根目录或无关目录。
- 如果 skill 涉及付费 API、外部写操作或高风险副作用，要在正文中写清确认条件、批量策略、速率限制和重试规则。
- 中文说明优先，英文保留给稳定 slug、命令、路径、参数、环境变量和 API 名称。
