# Natural Chinese · 自然中文

一个中文写作与润色 skill：去掉翻译腔、冗词和生硬句式，让文字自然、直接，同时保留原意、事实和作者语气。

规则根据提供的中文写作材料整理，包含 26 组编辑方法。覆盖多余成分、词语滥用、无效限定、抽象词和句式问题，每组都有改写示例与适用边界。

## 示例

原文：

> 当他看见我回来的时候，他就向我奔来。我们进行了为期三日的研究，最后作出了采用第二套方案的决定。

改写：

> 看见我回来，他就向我奔来。我们研究了三天，最后决定采用第二套方案。

这些规则需要按语境使用。例如，“他笑着说”中的“着”应当保留，“最早的记录之一”也不能删成“最早的记录”。

## 安装

将仓库中的 `skills/natural-chinese` 整个目录复制到所用工具的 skill 目录。目录内的 `SKILL.md` 是入口，`references` 保存详细规则，`agents/openai.yaml` 提供 Codex 界面信息。

在仓库根目录执行以下命令，可安装到 Codex 的个人 skill 目录；如果同名目录已存在，命令会停止，不覆盖现有版本。

```sh
python3 - <<'PY'
import os
import shutil
from pathlib import Path

codex_dir = Path(os.environ.get('CODEX_HOME') or Path.home() / '.codex').expanduser()
target = codex_dir / 'skills' / 'natural-chinese'
shutil.copytree(Path('skills/natural-chinese'), target)
print(f'已安装：{target}')
PY
```

## 使用

```text
请用 $natural-chinese 润色下面这段中文，保留原意和语气：
……
```

```text
请用 $natural-chinese 检查这段中译文的翻译腔，列出原句、建议和理由：
……
```

```text
请用 $natural-chinese 根据以下要点起草一段产品说明，保留技术术语：
……
```

默认交付改写正文；需要修改说明或前后对照时，在请求里说明。修改文件时，默认另存修订稿，除非用户指定覆盖。

## 文件

- [SKILL.md](skills/natural-chinese/SKILL.md)：适用范围、判断尺度与交付方式。
- [改写规则](skills/natural-chinese/references/editing-rules.md)：26 组规则、示例和保留条件。
- [界面配置](skills/natural-chinese/agents/openai.yaml)：名称、简介和默认提示语。

这套方法不把常用词列成禁用词，也不以词频判定写作质量；它不承担事实核查、词源考证或作者身份判断。
