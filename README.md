# daniel skill

基于 Daniel（GitHub [danielfbm](https://github.com/danielfbm)）公开代码与 review 样本整理的实现、重构和代码评审技能。

这是独立整理的非官方技能，与 Daniel 及相关项目没有隶属关系，也未获得其背书。它提炼有公开证据支持的工程方法，不模仿身份，也不声称代表其全部或永久偏好。

## 关注什么

- 保留已有行为契约，沿调用链检查 diff 外的影响
- 用能区分正确与错误实现的回归测试验证修改
- 复用已有实现，做最小必要变更，保持默认值可移植
- 区分阻塞问题与可后续建议，明确验证范围和限制

## 安装

在支持从 GitHub 安装技能的工具中，提供本仓库链接并请求安装 `daniel-skill`：

https://github.com/hawkli-1994/daniel-skill

对于使用本地 `$CODEX_HOME/skills` 目录的 Codex，可将仓库克隆到一个新的技能目录：

```sh
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone https://github.com/hawkli-1994/daniel-skill.git \
  "${CODEX_HOME:-$HOME/.codex}/skills/daniel-skill"
```

若目标目录已经存在，先检查已有版本，不要直接覆盖。不同产品的技能安装方式可能不同，请按该产品支持的流程操作。

## 使用

安装后，可以直接请求：

- “用 daniel skill review 这个 PR，只输出有证据的问题”
- “用 daniel skill 实现这次修改，重点检查行为回归和测试有效性”
- “用 $daniel-skill 重构这段代码，保留现有行为”

仅请求 review 时，技能要求保持只读；发布评论、提交代码或操作 PR 状态需要另外的明确授权。

## 文件

- [SKILL.md](SKILL.md)：技能入口与工作方法
- [agents/openai.yaml](agents/openai.yaml)：显示名称、提示词和技能元数据
- [references/evidence.md](references/evidence.md)：公开来源、日期、证据强弱与归因限制
- [references/examples.md](references/examples.md)：本技能编写的教学示例，并非 Daniel 原话或真实代码

## 来源与边界

资料截至 2026-10-06，来自公开 GitHub 评论、PR 和代码。完整出处见 [证据说明](references/evidence.md)，涵盖 tektoncd/cli、tektoncd/pipeline、AlaudaDevops/toolbox、AlaudaDevops/run-actions，以及 danielfbm 的相关仓库。

直接评论、账号发起或整合的代码、以及本技能的归纳建议分别标注。公开协作或 AI 辅助代码不代表每行均由本人手写；项目当前规范和用户的具体要求始终优先。
