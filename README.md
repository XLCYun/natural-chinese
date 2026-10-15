# Natural Chinese · 自然中文

一份大模型每次输出中文时都应参考的表达指南，以 `natural-chinese` skill 形式提供。让回答自然、直接、准确，减少翻译腔、冗词和生硬句式。

普通问答、技术解释、进度更新、总结、文件中的中文说明，以及文章写作和修改，都在适用范围内。无需用户说“帮我润色”；一句中文短答和中英混合内容中的中文也应参考。

指南包含 26 组表达规则，覆盖多余成分、词语滥用、无效限定、抽象词和句式问题，每组都有示例与适用边界。它指导如何组织中文，任务内容、输出格式和篇幅仍按用户要求处理。

## 示例

原文：

> 当他看见我回来的时候，他就向我奔来。我们进行了为期三日的研究，最后作出了采用第二套方案的决定。

改写：

> 看见我回来，他就向我奔来。我们研究了三天，最后决定采用第二套方案。

这些规则需要按语境使用。例如，“他笑着说”中的“着”应当保留，“最早的记录之一”也不能删成“最早的记录”。

## 安装并启用

将仓库中的 `skills/natural-chinese` 整个目录复制到所用工具的 skill 目录。目录内的 `SKILL.md` 是入口，`references` 保存详细规则，`agents/openai.yaml` 提供 Codex 界面信息。

在仓库根目录执行以下命令，可安装到 Codex 的个人 skill 目录 `~/.agents/skills`；如果同名目录已存在，命令会停止，不覆盖现有版本。目录位置见 [OpenAI 官方 skill 文档](https://learn.chatgpt.com/docs/build-skills)。

```sh
python3 - <<'PY'
import shutil
from pathlib import Path

target = Path.home() / '.agents' / 'skills' / 'natural-chinese'
shutil.copytree(Path('skills/natural-chinese'), target)
print(f'已安装：{target}')
PY
```

### 将“每次输出中文”设为常驻要求

Skill 的描述已把“输出中文”设为触发条件，界面配置也显式允许自动调用。但自动匹配仍由模型选择，`allow_implicit_invocation: true` 不是每次运行的强制钩子。参见 [官方触发机制](https://learn.chatgpt.com/docs/build-skills#how-chatgpt-and-codex-use-skills)。

要将本指南作为持续要求，安装后把以下片段加入宿主始终加载的指令。在 Codex 中，可加入全局 `~/.codex/AGENTS.md`；设置了 `CODEX_HOME` 时，使用该目录下的 `AGENTS.md`。若同层已有非空 `AGENTS.override.md`，应合并到实际生效的文件，保留其他规则。发现顺序见 [官方 AGENTS.md 文档](https://learn.chatgpt.com/docs/agent-configuration/agents-md)。

```markdown
## 中文表达

每次生成、修改或发送面向用户的中文内容前，都必须参考 natural-chinese 指南。
读取 ~/.agents/skills/natural-chinese/SKILL.md 并应用其表达规则；当前上下文已读取时直接沿用。
这适用于普通回答、追问、进度说明、最终回复及文件中的中文，不需要用户提出润色要求。
正常完成当前任务，只调整中文表达；保留事实、必要限定、术语、原样引用和要求的输出格式。
```

若安装在其他目录，将片段中的路径改成实际位置。其他支持读取文件的模型工具，也可在其常驻指令中引用同一份 `SKILL.md`；无法读取文件时，将指南正文加入工具的持久指令，并按需附上详细规则。

### 日常使用

启用常驻要求后，正常提问即可，例如：

```text
用中文解释一下这个报错，以及接下来怎么排查。
```

```text
总结当前进度，说明已经完成什么、还差什么。
```

临时显式调用也可以：

```text
请遵循 $natural-chinese，用中文回答下面的问题：……
```

需要润色或前后对照时，再明确提出对应任务。普通问答不会因为使用本指南而变成一份改稿报告。

## 文件

- [SKILL.md](skills/natural-chinese/SKILL.md)：中文输出的触发范围、表达习惯与判断尺度。
- [中文表达规则](skills/natural-chinese/references/editing-rules.md)：26 组规则、示例和保留条件。
- [界面配置](skills/natural-chinese/agents/openai.yaml)：名称、简介、默认提示语与自动调用设置。

这套方法不把常用词列成禁用词，也不以词频判定写作质量；它不承担事实核查、词源考证或作者身份判断。
