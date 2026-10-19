# Amplify AI Skills

**把模糊想法变成清晰、可用的结果。**

一组面向人与 AI 协作的 10 个 Agent Skills。无论你卡在提问、查证、决策、写作，还是修改已有成果，都可以从当前问题出发，找到合适的技能。

**语言：** 简体中文 · [English](README.en.md)

## 从当前卡点开始

| 你现在需要…… | 先用 | 你会得到 |
| --- | --- | --- |
| 把零散想法整理成明确需求 | [`clarify`](skills/amplify-ai-clarify/SKILL.md) | 清晰的需求或可继续执行的任务 |
| 把目标想得更大、更深、更广 | [`ambition`](skills/amplify-ai-ambition/SKILL.md) | 更有价值、可落地、可检验的任务表述 |
| 排优先级、定顺序或调整安排 | [`plan`](skills/amplify-ai-plan/SKILL.md) | 考虑依赖与取舍的行动计划 |
| 在几个方案中做选择 | [`decide`](skills/amplify-ai-decide/SKILL.md) | 依据目标和约束的建议 |
| 研究一个尚不清楚的问题 | [`research`](skills/amplify-ai-research/SKILL.md) | 有出处的答案与关键限制 |
| 从已有材料中提炼重点 | [`distill`](skills/amplify-ai-distill/SKILL.md) | 保留条件、分歧与出处的摘要 |
| 把意思写成能直接使用的文字 | [`write`](skills/amplify-ai-write/SKILL.md) | 适合读者和场合的成稿 |
| 核验主张、引用、数字或代码结果 | [`verification`](skills/amplify-ai-verification/SKILL.md) | 有证据边界的核验结论 |
| 按反馈修改已有成果 | [`refine`](skills/amplify-ai-refine/SKILL.md) | 保留有效内容的定向修改 |
| 帮特定受众理解一个主题 | [`explain`](skills/amplify-ai-explain/SKILL.md) | 适合理解目标的解释或演示 |

> **选用原则：** 先判断卡点，再选技能；一个技能能完成时，无需为了凑流程串用多个。

## 快速上手

每个技能都是以 `SKILL.md` 为入口的独立目录；技能本身无需安装依赖或配置 API key。在本仓库根目录执行：

**Codex：安装全部技能**

```bash
mkdir -p "$HOME/.agents/skills"
cp -R skills/amplify-ai-* "$HOME/.agents/skills/"
```

只安装一个技能时，例如 `plan`：

```bash
cp -R skills/amplify-ai-plan "$HOME/.agents/skills/"
```

**Claude Code：安装全部技能**

```bash
mkdir -p "$HOME/.claude/skills"
cp -R skills/amplify-ai-* "$HOME/.claude/skills/"
```

在 Claude Code 项目内使用时，也可以复制到该项目的 `.claude/skills/`。其他宿主请放入其读取 skills 的目录，或让 agent 直接读取 `skills/<name>/SKILL.md`；具体加载方式以宿主文档为准。

安装后直接描述任务，或显式点名技能，例如：

> 用 `amplify-ai-plan` 帮我把这项工作排出优先级和下一步。

宿主是否自动识别技能，取决于它的 skills 支持与配置。

## 技能如何配合

| 常见路径 | 适用情况 |
| --- | --- |
| `clarify` → `plan` / `decide` | 先明确目标，再安排工作或选择方案 |
| `research` → `verification` → `distill` / `write` | 先建立答案，再核查关键内容并整理成可用形式 |
| `write` → `refine` | 从意图写出初稿，再按反馈修改 |
| `explain` | 以理解为目标，按受众选择文字、图表、网页或视频 |

几个容易混淆的边界：

- **`clarify` / `distill`：** 前者理清需求或问法；后者整理已有材料。
- **`research` / `verification`：** 前者调查未知问题；后者核查已有主张或结果。
- **`write` / `refine`：** 前者从意图和素材成稿；后者按反馈修改已有产物。
- **`write` / `explain`：** 前者交付可直接使用的文字；后者帮助受众理解主题。

## 仓库结构与许可

- [`skills/`](skills/)：10 个可独立使用的技能目录，包含各自的 `SKILL.md` 和许可证。
- [`LICENSE`](LICENSE)：仓库的 MIT 许可证。使用单个技能时，请一并查看该技能目录中的许可证。

更新技能时重新复制对应目录；删除安装目录中的对应技能即可卸载。
