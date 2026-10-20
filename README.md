# daily-skills

日常使用的 Codex Skills 集合，沉淀可复用的工作流程与自动化经验。

每个 skill 聚焦一个具体任务，说明适用场景、操作流程和结果核验方式。内容采用通用规则，不绑定个人路径、固定集数或某一次会话。

## 技能列表

| Skill | 用途 |
| --- | --- |
| [bilibili-downkyi-download](skills/bilibili-downkyi-download/SKILL.md) | 核对 B 站系列集数、导出单集链接，通过 DownKyi 逐集添加下载，并简要提示低画质或疑似低画质版本。 |

## 目录结构

```text
daily-skills/
├── README.md
└── skills/
    └── bilibili-downkyi-download/
        ├── SKILL.md
        └── agents/
            └── openai.yaml
```

`SKILL.md` 包含技能名称、适用场景和执行说明；`agents/openai.yaml` 提供界面展示名称和简介。

## 安装与使用

在 Codex 中让内置的 `$skill-installer` 安装所需技能，例如：

```text
使用 $skill-installer 安装这个 skill：
https://github.com/fatebugs/daily-skills/tree/main/skills/bilibili-downkyi-download
```

安装后可用 `$bilibili-downkyi-download` 显式调用。如果安装后没有显示，可重启 Codex 后再次检查。技能安装与发现机制见 [OpenAI 官方 Skills 文档](https://developers.openai.com/codex/skills/)。

调用示例：

```text
使用 $bilibili-downkyi-download，查看当前浏览器中的这个系列，
从第 10 集检查到最新一集，排除合集并导出单集链接，
然后用 DownKyi 添加下载，最后简要告诉我是否有低画质版本。
```

也可以只执行其中一个阶段，例如核对缺集、导出链接或继续添加尚未处理的下载任务。起止集数、已处理条目和画质要求以本次请求为准。

## B 站下载技能的工作流程

1. 核对指定系列与集数范围，排除合集，识别缺集和重复条目。
2. 按需导出 TXT：按数字集数升序，每行一个单集链接。
3. 在 DownKyi 中逐条搜索、进入详情、下载选中项，并核实任务已添加。
4. 记录进度，跳过已处理条目，避免重复添加。
5. 简短汇报实际完成范围，以及低画质或疑似低画质的集数。

该技能需要当前 Codex 环境具备相应的网页读取和桌面操作能力，并能访问已配置好的 DownKyi。Skill 本身不包含下载器或浏览器控制组件。

“已加入下载队列”和“下载已完成”会分别表述。画质优先依据实际显示的选项或媒体信息判断；仅凭文件体积较小不会直接认定低画质。默认流程到下载状态与画质提示为止，不附带封面处理、文件重命名或完整解码检查。

## 添加新技能

在 `skills/` 下新增独立目录，编写对应的 `SKILL.md`，并更新上方技能列表。确有需要时再加入脚本、参考资料或资源文件。

- 使用简短明确的技能名称，写清适用场景。
- 保留可复用的判断规则和必要示例，避免固定个人路径与历史任务数据。
- 区分实际操作成功、已核验结果和仍不确定的状态。
- 根据真实使用反馈改进，保持单个技能的范围清晰。
