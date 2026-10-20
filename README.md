# daily-skills

日常使用的 Codex Skills 集合，沉淀可复用的工作流程与自动化经验。

每个 skill 聚焦一个具体任务，说明适用场景、操作流程和结果核验方式。内容采用通用规则，不绑定个人路径、固定集数或某一次会话。

## 技能列表

| Skill | 用途 |
| --- | --- |
| [bilibili-downkyi-download](skills/bilibili-downkyi-download/SKILL.md) | 核对 B 站系列集数、导出单集链接，通过 DownKyi 逐集添加下载，并简要提示低画质或疑似低画质版本。 |
| [tmdb-episode-manager](skills/tmdb-episode-manager/SKILL.md) | 根据来源资料核对、创建、补齐和校正 TMDB 分集信息。 |
| [tmdb-still-uploader](skills/tmdb-still-uploader/SKILL.md) | 按分集编号匹配本地图片，逐集上传并核验 TMDB 剧照。 |

## 目录结构

```text
daily-skills/
├── README.md
└── skills/
    ├── bilibili-downkyi-download/
    ├── tmdb-episode-manager/
    └── tmdb-still-uploader/
```

每个 skill 目录包含 `SKILL.md`；如果需要界面展示信息，还包含 `agents/openai.yaml`。

## 安装与使用

在 Codex 中让内置的 `$skill-installer` 安装所需技能，例如：

```text
使用 $skill-installer 安装这个 skill：
https://github.com/fatebugs/daily-skills/tree/main/skills/tmdb-episode-manager
```

安装后可分别使用 `$tmdb-episode-manager` 或 `$tmdb-still-uploader` 显式调用。如果安装后没有显示，可重启 Codex 后再次检查。技能安装与发现机制见 [OpenAI 官方 Skills 文档](https://developers.openai.com/codex/skills/)。

## 两个 TMDB 技能的边界

`tmdb-episode-manager` 负责核对来源、识别漏集、创建新集、顺延编号，以及校正标题、首播日期和时长。它会区分“表单已填写”“已保存”和“刷新后已复核”。

`tmdb-still-uploader` 只负责给已有分集上传本地剧照，按集号建立精确文件映射，确认图片条目出现后再进入下一集。它不会创建分集，也不会修改分集元数据；语言设置只有在用户明确要求时才处理。

两个技能都支持断点记录、跳过已完成条目和报告异常集数，避免批量任务重复操作。

## 添加新技能

在 `skills/` 下新增独立目录，编写对应的 `SKILL.md`，并更新上方技能列表。确有需要时再加入脚本、参考资料或资源文件。

- 使用简短明确的技能名称，写清适用场景。
- 保留可复用的判断规则和必要示例，避免固定个人路径与历史任务数据。
- 区分实际操作成功、已核验结果和仍不确定的状态。
- 根据真实使用反馈改进，保持单个技能的范围清晰。
