# 组装规则

## 目录结构

最小可用 Skill：

```text
<skill-root>/<skill-name>/
└── SKILL.md
```

按需补充：

- `references/`：详细规则、检查清单、变体说明
- `assets/`：输出模板、固定骨架、最终产物素材
- `scripts/`：确定性代码、CLI、可复用实现

## 文件职责

- `SKILL.md`：YAML 头部 + 路由、流程、约束
- `references/*.md`：只在命中后按需读取的详细说明
- `assets/*`：用于填充或复制的输出模板
- `scripts/*`：真正可执行或可复用的代码

## `scripts/` 规则

- 只要 Skill 需要代码，就把代码收敛到 `scripts/`。
- 入口、核心实现、辅助模块都应放在 `scripts/` 下，而不是散落在别的包目录。
- 只有在确有必要时才拆 `*_core.py`；如果只是很薄的一层，可直接并回主入口脚本。

## 组合模式的拆分

- 主模式决定 `SKILL.md` 的整体流程和 `metadata.pattern`。
- 次级模式不要写成第二套完整流程，而是拆成某一步的局部说明。
- 局部说明优先放进对应的 `references/` 或 `assets/`，并在该步骤显式写“此时再读取”。
- 不要为了“支持组合模式”就提前创建一整套暂时不会被读取的 supporting files。
- 如果组合后需要的 supporting files 已经接近两套独立 Skill，优先拆成两个 skill。

## YAML 头部优先

- 先保证 `SKILL.md` 头部完整、合法、可路由，再考虑 supporting files。
- `name` 和目录名保持一致。
- `description` 优先写触发条件，不要写成 README 简介。
- 可选字段只在确有信息增量时才补。

## 平台专属文件

- 通用 Skill 不预设任何平台专属 companion 文件。
- 只有当用户明确指定宿主产品时，才额外补该产品要求的配置文件。
- 平台专属文件不应反过来主导 Skill 的核心结构。

## 编写风格

- 中文说明优先，英文保留给稳定标识。
- 一份文件只做一件事。
- 不要补 README、CHANGELOG、安装教程等额外文档。
- 如果是升级已有 skill，优先最小改动，不要无意义重写。
