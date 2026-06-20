# AGENTS.md

## 工作区定位

本仓库是剧本开发与视频化生产工作区。正式剧本项目必须进入 `projects/<project-slug>/`，每个项目独立维护故事事实、角色、场景、素材、镜头节拍和视频交付。

当前正式项目：

- `projects/frozen-rebirth-revenge/PROJECT.md`：极寒重生复仇爽剧项目入口。

## Agent 工作规则

- superpower 执行计划默认使用 Subagent-Driven 方式。
- 处理项目任务前，先读取对应 `projects/<project-slug>/PROJECT.md`。
- 通用剧本规范优先使用个人 skill `script-development-director`。
- Seedance 2.0 视频提示词优先使用 `seedance2-video-director`。
- 项目事实只从当前项目目录读取，不混用其他剧本的人物、素材、场景和视频片段。
- 不要直接覆盖已有正文版本；需要大改时优先新建临时迭代稿，除非用户明确要求覆盖。
- 保留用户已有改动，不要回滚未由你创建的文件。
- 涉及 `.env` 时只读取变量，不输出 API key。

## 项目结构

标准项目目录：

```text
projects/<project-slug>/          # 单个剧本项目目录，slug 使用小写英文、数字和连字符
├── PROJECT.md                    # 项目入口：定位、状态、正典文件和交付入口
├── bible.md                      # 项目设定总纲：世界观、人物关系、冲突和连续性规则
├── episodes/                     # 单集剧本目录，保存 episode-xx-script.md
├── assets/                       # 素材目录，保存素材 brief、索引、生图提示词和最终图片
├── storyboards/                  # 镜头节拍目录，服务 Seedance 的段内时间线和画面动作
├── video-generation/             # 视频生成交付目录，保存可直接输入模型的 handoff
├── reviews/                      # 审查和复盘目录，保存质量检查、素材总览和问题记录
└── research/                     # 可选研究目录，保存题材、竞品、平台和资料调研
```

当前项目关键文件：

- `projects/frozen-rebirth-revenge/PROJECT.md`：项目入口和正典索引。
- `projects/frozen-rebirth-revenge/bible.md`：设定总纲。
- `projects/frozen-rebirth-revenge/episodes/episode-01-script.md`：第一集正典剧本。
- `projects/frozen-rebirth-revenge/assets/asset-briefs.md`：人物、场景、道具素材 brief。
- `projects/frozen-rebirth-revenge/assets/_asset-index.md`：素材索引。
- `projects/frozen-rebirth-revenge/assets/image-generation-prompts.md`：生图提示词。
- `projects/frozen-rebirth-revenge/storyboards/episode-01-shot-beats.md`：Seedance 镜头节拍。
- `projects/frozen-rebirth-revenge/video-generation/episode-01-handoff.md`：视频生成交付。
- `projects/frozen-rebirth-revenge/reviews/episode-01-quality-check.md`：质量检查。

## 剧本生产流程

每个项目按以下顺序推进：

1. 项目开工：锁定类型、目标平台、核心卖点、主角欲望、敌人/阻力和结尾状态。
2. 项目 bible：整理世界观、人物关系、核心冲突、爽点机制和连续性规则。
3. 单集剧本：写可拍场次、动作、对白、道具变化和情绪转折。
4. 剧本审查：检查因果、爽点、可拍性、节奏、人物动机和结尾钩子。
5. 素材 brief：规划人物设定图、场景图、道具图和必要关键帧。
6. 生图与索引：素材进入项目 `assets/` 根目录，用户确认后标记可用。
7. 镜头节拍：把剧本拆成 Seedance 可执行的时间线、动作、镜头和声音。
8. 视频交付：输出可直接输入视频模型的提示词、素材引用和禁止项。

## 素材规则

- 图片素材统一放在项目 `assets/` 根目录，不按人物、场景、集数分多层级保存最终交接图。
- 镜头节拍和视频交接引用素材使用 `@中文素材名`。
- 实际文件名必须与 `@素材名` 去掉 `@` 后一致，例如 `@暴雪楼道场景图` 对应 `assets/暴雪楼道场景图.png`。
- 单张场景图只对应一个场景或一个空间功能；不要把多个场景、动线标记、镜头框、箭头和说明文字拼进给视频模型使用的参考图。
- 已确认素材才能进入视频提示词；废稿、旧版本和未确认图不得混入正式交付。

## Seedance 交付规则

- 视频交付只保留模型可执行字段：素材、时长、时间线、动作、镜头、声音、提示词、禁止项。
- “镜头节拍”是一个视频段内部的时间线，不等于全部独立生成任务。
- 视频延长只在同一空间、同一动作链、同一镜头方向需要承接上一段末帧时使用；换时间、换空间、主观闪回或情绪断裂时独立生成。
- 画面风格词必须落到主体、空间、光影、镜头、动作和时间线，不用空泛形容词堆叠。

## 质量闸门

- 没有 PROJECT 和 bible，不进入正式剧本。
- 剧本未审查通过，不生成正式人物图、场景图、关键帧、镜头节拍或视频提示词。
- 素材名、索引名、提示词引用名和文件名必须一致。
- 视频交付前检查每段是否有明确画面目标、动作节拍、镜头运动、声音/对白和禁止项。
